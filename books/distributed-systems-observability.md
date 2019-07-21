# [Distributed Systems Observability](https://www.goodreads.com/book/show/40182805-distributed-systems-observability)

- [The need of observability](#the-need-of-observability)
- [Monitoring and observability](#monitoring-and-observability)
- [Coding and testing for observability](#coding-and-testing-for-observability)
  - [Testing for failure](#testing-for-failure)
- [The three pillars of observability](#the-three-pillars-of-observability)
  - [Event logs](#event-logs)
  - [Metrics](#metrics)
  - [Tracing](#tracing)

Most failures not addressed by application layers will arise from the complex interactions between various applications.

Observability isn't purely an operational concern.

## The need of observability

**Observability is not just about logs, metrics and traces it's about bringing better visibility into systems.**

Observability is a property of the system. It does acknowledge the following
- No complex system is ever fully healthy.
- Distributed systems are unpredictable.
- It's impossible to predict the state of different parts of the system.
- Failure needs to be embraced.
- Easy debugging is fundamental.

Observability is a feature that needs to be enshrined into a system.
- Lends itself well to being tested in a realistic manner (a degree of testing in production).
- Failure modes can be surfaced during the time of testing.
- Deployments can happen incrementally so the rollback can be triggered if a key of metrics deviate from the baseline.
- Report enough data points, so the system can be understood.

## Monitoring and observability

**Observability is a superset of monitoring.** It provides highly granular insights into the implicit failure modes of the system. An observable system provides contexts about its inner workings.

**Monitoring reports the overall health of systems and derives alerts**

> ### Blackbox and whitebox monitoring
> _Blackbox monitoring_ refers to observing a system from the outside. Useful for identify the _symptoms_ of a problem like "error rate is up".
> _Whitebox monitoring_ refers to techniques of reporting data form inside a system.

Monitoring data should always provide a bird's-eye view of the overall health of a distributed system by recording and exposing high-level metrics over time across all components of the system.

**All alerts need to be _actionable_.**

A good set of metrics are the USE metrics and the RED metrics.
* USE methodology is for analysing system performance like utilisation, saturation, errors of resources, free memory, CPU or device errors.
* RED methodology is about application level metrics like request rate, error rate, and duration of the requests.

Debugging is often an iterative process and involves
* Start with a high-level metric
* Drill down observations
* Make the right deductions
* Testing the theory

Observability doesn't obviate the need for careful thought. The process of knowing what information to examine (observations), requires a good understanding of the system and domain, as well as a good sense of intuition.

## Coding and testing for observability

The idea of experimenting with live traffic is either seen as the preserve of operations engineers or is something that's met with alarm. Some amount of regression testing to post-production monitoring requires coding and testing for failure.

Acknowledging that systems will fail, being able to debug such failures is of paramount importance, and embedding debuggability into the system from the ground up.

Understanding service dependencies and abstractions better, allows you to improve reliability massively just by changing a single line of configuration.

### Testing for failure

Unit tests only ever test the behaviour of a system against specified set of inputs.

End-to-end testing might allow for some degree of holistic testing of the system, but complex systems fail in complex ways.

The tooling aimed to understand the behaviour of our services in production does not obviate the need for pre-production testing.

**Certain types of failures can only be surfaced in the production environment.**

| Pre-production         | Deploy              | Release            | Post-release           |
|------------------------|---------------------|--------------------|------------------------|
| - Unit tests           | - Integration tests | - Canarying        | - Teeing               |
| - Functional tests     | - Tap compare       | - Monitoring       | - Profiling            |
| - Component tests      | - Load tests        | - Traffic shaping  | - Logs/events          |
| - Stress tests         | - Shadowing         | - Feature flagging | - Chaos testing        |
| - Static analysis      | - Soak tests        |                    | - Monitoring           |
| - Property based tests |                     |                    | - A/B tests            |
| - Coverage tests       |                     |                    | - Tracing              |
| - Benchmark tests      |                     |                    | - Dynamic exploration  |
| - Regression tests     |                     |                    | - Real user monitoring |
| - Contract tests       |                     |                    | - Auditing             |
| - Lint tests           |                     |                    | - On-call experience   |
| - Acceptance tests     |                     |                    |                        |
| - Mutation tests       |                     |                    |                        |
| - Smoke tests          |                     |                    |                        |
| - UI/UX tests          |                     |                    |                        |
| - Usability tests      |                     |                    |                        |
| - Penetration tests    |                     |                    |                        |
| - Threat modelling     |                     |                    |                        |

Testing in production (deploy, release and post-release phases) is impossible to do without measuring how the system under test is performing in production.

## The three pillars of observability

### Event logs

An _event log_ is an immutable, timestamped record of discrete events that happened over time. Usually a pair of a timestamp and a payload of some context. There are three forms: plain text, structured (peg: JSON) and binary (peg: Protobuf format in MySQL binlogs).

Event logs are especially helpful for uncovering emergent and unpredictable behaviours exhibited by components of a distributed system.

Traces and metrics are an abstraction built on top of logs.

**Pros:**
- Easiest to generate
- Easy to instrument

**Cons:**
- Suboptimal performance due to the overhead of logging.
- Messages can be lost unless one uses a protocol like RELP to guarantee delivery of messages.

Logging excessively has the capability to adversely affect application performance as a whole. A solution to this is to do _Sampling_, picking a small subset of the total population of event logs.

Raw logs are almost always normalised, filtered, and processed by a tool like Logstash, fluentd, Scribe or Heka before they're persisted in a data store like Elasticsearch or BigQuery. Logs might require further buffering in a broker like Kafka before they can be processed by Logstash.

Logs can also be the source for all analytics data, which has a tremendous utility from a business intelligence perspective. Complex queries can be made thanks to storing events. Events are structured key-value paris.

Most analytics pipelines use Kafka as an event bus. Sending enriched event data to Kafka allows one to search in real time over streams with KSQL, an SQL engine for Kafka. This data can be expired from the Kafka log regularly. There are alternatives like Humio, Honeycomb and Facebook's Scuba.

### Metrics

_Metrics_ are a numeric representation of data measured over intervals of time.

Since they are numbers, metrics enable longer retention of data as well as easier querying. They are perfectly suited to building dashboards that reflect historical trends stored in time-series databases.

Modern monitoring systems like Prometheus and newer versions of Graphite represent every time series using a metric name as well as additional key-value pairs called _labels_.

**Pros:**
- Metrics transfer and storage has a constant overhead. The cost doesn't increase in lockstep with user traffic. Storage increases with more permutations of label values tho.
- They are more malleable to mathematical, probabilistic, and statistical transformations such as sampling, aggregation, summarisation, and correlation. They are better suited to report the overall health of a system.
- Metrics are also better suited to trigger alerts.

**Cons:**
- They are _system_ scoped, making it hard to understand anything else other than what's happening inside a particular system.
- A single line doesn't give you much information about what happened to a request across all components of a system. Distributed tracing is a technique that addresses the problem of brining visibility into the lifetime of a request across several systems.

### Tracing

A _trace_ is a representation of a series of casually related distributed events that encode end-to-end request flow through a distributed system.

Traces identify specific points in an application, proxy, framework, library, runtime, middleware and anything else in the path of the request that represents:
- Forks in execution path
- A hop or a fan out across network or process boundaries.

A trace is a directed acyclic graph of _spans_, where the edges between spans are called _references_.

When a request begins, it's assigned a globally unique ID, which is then propagated through the request path, so that each point of instrumentation is able to insert or enrich metadata before passing the ID around to the next hop. Each hop along the flow is represented by a span. Each record emitted on each service are usually asynchronously logged to disk before being submitted out of band to a collector, which then can reconstruct the flow of execution.

Understanding request lifecycles makes it possible to debug requests spanning multiple services to pinpoint the source of increased latency or resource utilisation.

Zipkin and Jaeger are the two most popular OpenTracing-compliant open source distributed tracing solutions.

**Cons:**
- Traces are the hardest to retrofit into an existing infrastructure. Every component in the path of a request needs to be modified to propagate tracing information.
- It's not sufficient for developers to instrument just their own code alone.
- Challenging at places with polyglot architectures.

> #### Service mesh, a new hope
> Service meshes make integrating tracing functionality almost effortless as they implement tracing and stats collections at the proxy level. Applications will still need to forward headers to the next hop in the mesh, but no additional instrumentation is necessary.
