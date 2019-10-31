# [Mastering Chaos: A Netflix Guide to Microservices](https://www.youtube.com/watch?v=CZ3wIuvmHeM)

## Microservices basics

What microservices are not:
* **Monolithic code base.** Everyone was contributing to a single code base that was released once a week, when change introduced a problem it was difficult and slow to debug. Because so many changes were released on a single deploy.
* **Monolithic database.** When this went down, everything went down. Scaling it vertically was very expensive.
* **Tightly coupled architecture.** One of the most painful points was the lack of agility, everything was deeply interconnected.

What is a microservice: An evolutionary response
* Separation of concerns. Modularity, encapsulation
* Scalability. Horizontally scaling, workload partitioning
* Virtualisation and elasticity. Automated operations, on demand provisioning

Microservices as organs:
* Each organ has a purpose
* Organs form systems
* Systems form an organism

Microservices are an abstraction:
* You have a **service** that provides some functionality
* The service may need to access some persistence mechanism like a **database**
* You may provide **service client** for accessing data operations
* You may provide an **cache for your client** (peg: [EVCache](https://github.com/Netflix/EVCache))
* You may need to provide some orchestration between the client and the cached client, so you may need to really provide a **client library** that will go to the cache first, and if it fails will go for the client that will hit the microservice and persistence layer and then backfill the cache for the next call
* All this will have to be embedded within the **client application** that wants to use the 

From the consuming application the client library, that includes the service client cache, the service client, the service and the database is the microservice. Is not a simple state thing.

## Challenges and solutions

### Dependency

#### Infra-service request

Everything is great until something breaks.
* Network latency, congestion, failure.
* Logical or scaling failure.

Cascading failure, one service fails without defences it can cascade and take down your entire network.

Solution: [Hystrix](https://github.com/Netflix/Hystrix)
* Structured way of handling timeouts and retries
* Fallbacks, if I cannot call a service, can I return some static response instead (degraded service) to allow the customer to continue using the product
* Isolated threadpools and the concept of circuits. If you keep hammering the service and it keeps failing, maybe you should stop calling it and fail fast returning the fallback

How do you know if it works at scale? Netflix created [FIT](https://medium.com/netflix-techblog/fit-failure-injection-testing-35d8e2a9bb2) (Fault Injection Testing) to test this. It inject failure information metadata to [Zuul](https://github.com/Netflix/zuul), and this is carried through the network.
* Synthetic transactions
* Override by device or account
* % of live traffic up to 100%
* Enforced throughout the call path

How do we constraint testing scope? (So you are not testing millions of permutations, or downstream dependencies of the services you test). To address this Netflix defined the critical microservices to have basic functionality to work, which is not all of them, and test only those (by blacklisting all of the other services that are not critical). This has worked great to make sure that the service actually functions when all those dependencies go away. This is a much simpler approach than doing point-to-point interactions.

Client libraries
* Many clients
* Common business logic
* Common access patterns

Trade-offs for client libraries
* Heap consumption
* Logical defects
* Transitive dependencies

We can limit the client libraries, try to simplify them as much as possible.

Persistence
* CAP theorem

In the presence of a network partition, you must choose between between consistency and availability.

Netflix chose availability via Cassandra, systems are eventually consistent.

Infrastructure
Do not put all your eggs into one basket. [You can go multi-region](https://www.infoq.com/presentations/netflix-failure-multiple-regions/).

### Scale

#### Stateless services

* Not a cache or a database
* Frequently accessed metadata
* No instance affinity
* Loss a node is non-event, you can replace a node at no cost

Auto scaling groups is fundamental for microservices, advantages
* Compute efficiency, on-demand capacity
* Node failure, nodes gets replaced easily
* Traffic spikes, DDoS attack, etc.
* Performance bugs, auto-scaling allows you to absorb damage while figuring out what happened

Surviving instance failure, thanks to Chaos Monkey (losing individual nodes).

#### Stateful services

* Databases and caches
* Custom apps which hold large amounts of data
* Loss of a node is a notable event, it could take hours to recover

Redundancy is fundamental, EVCache similar to memcache but it writes to several zones for redundancy

#### Hybrid services

It's easy to take EVCache for granted
* 30 million requests/sec
* 2 trillion requests per day globally
* Hundreds of billions of objects
* Tens of thousands of memcached instances
* It consistency scales in a linear way, no matter the load. Milliseconds of latency per requests

Problem is you may rely too much on EVCache. Solutions
* Workload partitioning, split cache by workload (real-time vs batch processes)
* Request-level caching, so you are not repeat hitting the service over and over. Make the first hit expensive and the rest of them free through the lifecycle of the application
* Secure token fallback, embed a secure token through the requests. If the subscriber service is unavailable, fallback to a datastore with that encrypted token so you have enough information to identify the customer and provide basic operation
* Chaos under load, use tools to test your architecture

### Variance within your architecture

The more variety you have in your system, the more complex and difficult to manage it becomes.

#### Operational drift, which happens over time

Unintentional, it happens eventually.

Over time
* Alert thresholds
* Timeouts, retries, fallbacks
* Throughput (RPS)

Across microservices
* Reliability best practices

The first time you talk with teams about this, they will be very enthusiastic; however, as this is tedious and repetitive, and is not related to product work, people will tend to avoid it.

They solved the cycle with continuous learning and automation. An incident gets a resolution, then a review happens, a remediation plan, some analysis, then extract some learning into best practice, then you automate wherever possible, then you drive adoption.

##### Production ready checklist

* Alerts
* Apache and Tomcat
* Automated canary analysis
* Autoscaling
* Chaos
* Consistent naming
* ELB config
* Healthcheck
* Immutable machine images
* Squeeze testing
* Staged, red/black deployments
* Timeouts, retries, fallbacks

#### Polyglot (new languages) and containers

Intentional variance.

The paved road, focused on Java and EC2
* Stash
* Nebula/Gradle
* BaseAMI/Ubuntu
* Jenkins
* Spinnaker
* Runtime platform

Some engineers went off road, building their own roads, doing stuff in Python, Ruby, NodeJS, each one of them provided value in some sense. When Docker was introduced, things went a bit wild.

#### Cost of variance

* Productivity tooling
* Insight and triage capabilities
* Base image fragmentation
* Node management
* Library/platform duplication
* Learning curve, production expertise

Instead of a single paved road, now we have multiple paved roads that makes life difficult for the teams that support engineering infrastructure.

The strategic stance to cost was to
* Raise awareness of costs
* Constraint centralised support, focus specially into JVM, and of course for Docker
* Prioritise by impact
* Seek reusable solutions

How do we achieve velocity with worrying about breaking things all the time?

Global cloud management and delivery, Spinnaker an automated delivery system.
* Conformity checks
* Red/black pipelines
* Automated canaries
* Staged deployments (one region at a time)
* Squeeze tests

## Organisation and architecture

Electronic Delivery, NRDP 1.x. Wasn't called Streaming yet.
  * Simple UI, "Queue Reader"
  * Collaborative design
  * XML payloads
  * Custom responses
  * Versioned firmware releases
  * Long cycles

In parallel the Netflix API, let a 1000 flowers bloom. It wasn't very successful but after that, it started to be used privately
  * Content Metadata
  * General REST API
  * JSON schema
  * HTTP response codes
  * OAuth security model (it was important for 3rd party apps)

Hybrid architecture, now we have these two edge services functioning in very different ways. Distinct in
* Services
* Protocols
* Schemas
* Security

There was a lot of friction between teams, as client developer you would have to change context all the time.

Josh: What is the right long term architecture?
Peter: Do you care about the organisational implications?

### Conway's law

Any piece of software reflects the organisational structure that produce it.

If you have four teams working on a compiler you will end up with a four pass compiler.

**This is not solutions first, this is organisation first.**

### Outcomes and lessons

By unifying these things around the client.

Outcomes
* Productivity and new capabilities
* Refactored organisation

Lessons
* Solutions first, team second
* Reconfigure teams to best support your architecture

---

Microservice architecture as complex and organic.

Health depends on discipline and injecting chaos.

Dependency
* Circuit breakers, fallbacks, chaos
* Simple clients
* Eventual consistency

Scale
* Auto-scaling
* Redundancy, avoid SPoF
* Partioned workloads
* Failure-driven design
* Chaos under load

Variance
* Engineered operations
* Understood cost of variance
* Prioritised support by impact

Change
* Automated delivery
* Integrated practices

Organisation and architecture
* Solutions first, team second
