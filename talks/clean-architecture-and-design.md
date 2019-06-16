# [Clean Architecture and Design](https://www.youtube.com/watch?v=Nsjsiz2A9mg)

A typical Ruby applications structure
* Controllers
* Logs
* Views
* ...

Why is not telling me what it does? How it behave?

**Frameworks have a tendency of structuring your code around web details.**

The web is a delivery mechanism. Why the application is formed up around on IO channel?

If we look at a picture of a library, we can understand that is a library. We don't see hammers and saws.

**Architecture is about intent!**

**Use-cases should drive the architecture.**

Example of a use case:

```
Create Order
Data: Customer ID, Shipment destination, Payment information, Customer contact info, Shipment mechanism
Primary course:
    1. Order clerk issues "Create Order" command with above data.
    2. System validates all data.
    3. System creates order and determines order-id.
    4. System delivers order-id to clerk.
Exception course: Validation error
    1. System deliver error message to clerk.
```

We don't care about details at use case level. It doesn't say _how_. Nothing is not about the IO channel, nothing about the use case to be web.

```
                         Request/Response that don't know anything about web
───────────────────┐
                   ├───► Boundary <i> ◄──┐
Delivery mechanism │                     ├─ Interactor ──► Entity
                   ├──|► Boundary <i> ◄|─┘
───────────────────┘
      ▲   Request/response translation for the delivery mechanism
      │ 
      │
     User (request/response for specific delivery mechanism

─────────────────── REQUEST ───────────────────►
◄────────────────── RESPONSE ───────────────────
```

## Interactors

These are the use cases. Objects that encodes the processing rules, and application specific business rules. Probably exposing an `execute` method to the outside world (Command Pattern).
The interactor tells the _Entities_ what to do.

## Entity

This are the objects that have the business logic.

## Boundary

These are interfaces. The interactor implements one of the interfaces, interactors implemented outputs and inputs.

---

Then the Web happened. After the 2.0 bubble crash, people were looking for anything that would help.

Rails was invented, you can build a website iterarively really fast. The Rails ways of thinking carries a lot of baggage with it

## MVC is not an architecture

```
View ═══► Model ◄──── Controller
```

* **Model**: small objects with mutable data
* **View**: has an observable behaviuour over the model, that changes the view
* **Controller**: would observe clicks and user input and modify the model
* **MVC goes wrong as a web architecture**.

Business objects becomes this thing, half controller half view, etc. Boundaries are not very well defined to do it properly

## Model-view presenter

```
               ║                                       ┌───► Entity
               ║                                       │
Presenter ─────║─────► Boundary ◄────── Interactor ────┼───► Entity
    │  │       ║          |                  │         │
    │  │       ║          └──────────┐       ▼         └───► Entity
    │  │       ║                     ├ Response Model
    │  └───────║─────────────────────┘                     
View Model     ║ 
    ▲          ║
    │          ║
  View         ║
```

Look about the direction of dependencies. Your delivery mechanism depends on your application.
The web (the delivery mechanism) is a plugin. Your application should not know about it.

```
    ┌──────────║───► Request model ◄───────────┐
    │          ║          ▲                    │
    │          ║          │                    │
Controller ────║───► Boundary <i> ◄|───┐       │
               ║                       ├─── Interactor
Presenter ─────║──|► Boundary <i> ◄────┘       │
    │          ║          │                    │
    │          ║          ▼                    │
    └──────────║───► Response model ◄──────────┘
```

All this is already testable, and decoupled. Plug-in architecture.

## Databases

They defined our industry for the last 30 years. The database have become the center of our applications. We have given too much importance to databases.

The reason we have databases is a hardware issue, if we could store data in memory, we wouldn't use databases. If you don't mutate state, we can increasingly store events, there is no need for transactions.

**The database is a detail!** Is just the thing that holds the data, we should treat it like a plugin.

```
               ┌───► Entity ◄───┐
               │                │
Interactor ────┼───► Entity ◄───┤
     │         │                │
     │         └───► Entity ◄───┤
     ▼                          │
Entity Gateway <i>              │
     ▲                ┌─────────┘
     │                │
══════════════════════════════════════
     │                │
Entity Gateway ├──────┘
Implementation ├───────► Database API
```

An object is not a bunch of data, an object is a bunch of methods. Data should be encapsulated. Your entities shouldn't expose their data for the database.

Below the line the main program, is a plugin. Where you have your factories, dependency injection container, etc.

**A good architecture allows major decisions to be deferred!** Decisions about the UI, the database, the framework, etc.

**A good architecture maximises the number of decisions not made.**

References:
* [Object-Oriented Software Engineering](https://www.goodreads.com/book/show/296981.Object_Oriented_Software_Engineering) by Ivar Jacobson.