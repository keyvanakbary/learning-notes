# [Grinding the monolith](https://www.youtube.com/watch?v=xxW_c_8AHiE)

## Monolith

Pros:
* Easier to deploy
* Easier to place and find stuff in

## Microservices

Cons:
* Operational complexity
* Partial failure

Pros:
* Independence of development
* Independence of scalability
* Building in smaller and simpler pieces

### We have heard the story before

Java Beans, COMM, COBRA
* Independent components, you can just buy and connectcomponents
* Decoupled and simple pieces

We can have software that works like Lego. But this hypothesis does not work in reality as there are many more dimensions (connections between components). Components may have hundreds or thousands of collaborators, we would need to have to have nth dimensional Lego bricks!

Maybe a better model would be Mycelium, a fungus where fractal roots communicate to each other in a way more complex way.

We can try to make a clear horizontal layered separation: UI, Application, Domain, Persistence. Try to repeat the pattern in vertical separations, but soon enough they will start coupling each other. We can make the thing even worse with operational monitoring, logging, etc.

Maybe the Layers architecture referred more to protocol stacks than to web applications, precisely because of the standarisation of interfaces between layers does not generally apply.

## Microservices

The key issue is around **safety** for different teams to operate independently. Issues from other teams should affect yours. Without this, you'll start adding checks, reviews, etc. "The Fear Cycle".

Safety failure in Monoliths

* Bad code has an unlimited span of effect (SQL leak will affect all code)
* Modifying shared code will affect other teams
* Semantic coupling, different concepts mixed under the same name. What works for one context, may not work for the other

All those make code changes slow. Many teams tried transformations towards microservices, 2/3s failed because impatience, unrealistic expectations, or hubris.

## Strategies to move towards microservices

### Clean then separate

Refactor to create interfaces between subdomains, then turn those into HTTP interfaces.

**Failed**
* You have to stop feature development
* You have the clean team is going slower than the feature teams that will make compromises to go faster (their work is throwaway)

### Entity services

You turn your key domain objects into services

**Failed**
* Transactionality problems. Microservices need to have behaviour
* Deployments are painful as redeploying a core entity service will affect a lot of clients
* Distributed monolith

### Project teams

Have a pool of people (contractors) do create services and throw them back to the pool once they finish.

**Failed**
* Favour deadlines (short term) over high quality code and architecture initiatives (long term)
* If you done your hard work, you should enjoy the fruit of the result. If not, you should leave with it and learn from it
* Better to have product teams (which can have projects)

### Clean-sheet design of a new services

Create new services from scratch

**Failed**
* We make the same mistakes over and over
* This system will always lag behind
* Optimism not supported by past evidence. What happened last time (unexpected issues) is most likely to happen this time

### The strangler

Intercept traffic to the existing system and replace pieces with new services. It is a transitional pattern.

**Partial success**

### Clone and slash

Clone the monolith for each team. Remove the code the team does not need. Transitional state. You will be sharing the DB for a long time.

**Success**

### Continual redesign/rebuild

Keep the presure on to keep redesigning, microservices are never done. Remove code and microservices, which is one of the main benefits of removing microservices.

**Success**

### Microservices by lifecycle

Each stage of the process has its own microservice, and each process/microservice passes the state to the next.

**Success**

### Transmit domain objects on the wire

Domain objects as the representation to transfer in APIs.

**Failure**
* Domain object coupled with the API, will be very difficult to evolve and change
* Makes it very difficult to handle multiple versions of APIs
* Leaks implementation details and internals of the service

Turn domain objects into hashmaps, lists, etc.

### Refactor to hexagons

Express the domain independently from integration and persistence implementation details.

**Success**

---

Think long-term, act short-term. Solve the problem in front of you.

---

References
- "Layers architecture": [Pattern oriented software architecture, vol 1](https://www.goodreads.com/book/show/85039.Pattern_Oriented_Software_Architecture_Volume_1)