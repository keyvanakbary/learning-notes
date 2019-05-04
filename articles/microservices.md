# [Microservices by Martin Fowler](https://www.martinfowler.com/articles/microservices.html)

Microservice architectural style is an approach to developing a single application as a suite of small services, each running in its own process and communicating with lightweight mechanisms, often an HTTP resource API.

Built around business capabilities.

## Monolith
- A monolithic application built as a single unit. All your logic for handling a request runs in a single process.
- A change made to a small part of the application, requires the entire monolith to be rebuilt and deployed.
- It's often hard to keep a good modular structure.
- Scaling requires scaling of the entire application rather than parts.

## Microservice
As well as the fact that services are independently deployable and scalable, each service also provides a firm module boundary.

### Characteristics

* **Componentization via Services.** Component is a unit of software that is independently replaceable and upgradeable. Libraries in-memory function calls, while services are out-of-process communicate via RPC or web requests. services are independently deployable. More explicit components. Services map to runtime processes, but that is only a first approximation. Downsides: Remote calls are more expensive than in-process calls.
* **Organized around Business Capabilities.** Broad-stack implementation of software for that business area, including user-interface. Siloed funcional teams creating layered architectures (silos) vs cross-functional team and softwar organised vs capabilities (Conways law). Micro-services are cross-functioal. The necessarily more explicit separation makes it easier to keep the team boundaries clear.
* **Products not Projects.** A team should own a product over its full lifetime, you build it you run it. The product mentality, ties in with the linkage to business capabilities. Rather than looking at the software as a set of functionality to be completed.
* **Smart endpoints and dumb pipes.** Microservices aim to be as decoupled and as cohesive as possible. Like Unix pipes (HTTP request-response and RESTish protocols), or messaging over lighweight message bus (RabbitMQ). Issue: The biggest issue in changing a monolith into microservices lies in changing the communication pattern.
* **Decentralised governance.** You can choose the apropriate technology for your service, no need to limit or standarise the technology across use cases. Prefer to use sharing battle-tested code as libraries.
* **Decentralised data management.** Conceptual model of the world will differ between systems. The concept of a Bounded Context in DDD. With microservices there is a natural correlation between service and context boundaries. Decentralise data storage decisions. Let each service manage their own data. This may introduce eventual consistency. Managing inconsistencies will be a challenge.
* **Infrastructure automation.** Once you have automated the deployment pipeline for monolith, doing the same for microservices won't be that hard. The operational landscape between the monolith and the microservices can be strikingly different.
* **Design for failure.** Applications need to be designed so they can tolerate the failure of services. Clients have to react gracefully on service failure. Detect failures quickly and recover the service automatically if possible. Sophisticated monitoring and logging setups, up/down dashboards, relevant metrics. Details on circtuit breakers, throughput, latency…
* **Evolutionary design.** Control changes in the application without slowing down change. Independent replacement and upgradeability. Evolve monoliths to miroservices, the core as the monolith and new services in microservices. Granular release planning. You only need to deploy services you modify, not all like in the monolith. Use versioning internally if necessary, but try to avoid it.

---

### Are microservices the future?

Worth serious consideration for enterprise applications.

The decay seen in monolith applications may be less likely with microservices architecture where boundaries are explicit and hard to patch around.
In the other hand, getting boundaries right is difficult and refactoring them is important. Refactoring a distributed architecture is more difficult as interface changes need to be coordinated.

Components may not compose cleanly, complexity from inside a component may move to the connections between components.
There is also a factor of team skill.

Probably you shouldn't start with a microservices architecture, instead begin with a monolith, keep it modular and split it into microservices once th emonolith becomes a problem.