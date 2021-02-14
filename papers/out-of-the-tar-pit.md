# [Out of the Tar Pit](http://curtclifton.net/papers/MoseleyMarks06a.pdf)

- [Complexity](#complexity)
  - [Simplicity is hard](#simplicity-is-hard)
- [Approaches to understanding](#approaches-to-understanding)
- [Causes of complexity](#causes-of-complexity)
  - [Complexity caused by state](#complexity-caused-by-state)
  - [Complexity caused by control](#complexity-caused-by-control)
  - [Complexity caused by code volume](#complexity-caused-by-code-volume)
  - [Other causes of complexity](#other-causes-of-complexity)
- [Classical approaches to managing complexity](#classical-approaches-to-managing-complexity)
  - [Object-orientation](#object-orientation)
  - [Functional programming](#functional-programming)
  - [Logic programming](#logic-programming)
- [Accidents and essence](#accidents-and-essence)
- [Recommended general approach](#recommended-general-approach)
  - [Ideal world](#ideal-world)
  - [Theoretical and practical limitations](#theoretical-and-practical-limitations)
- [The relational model](#the-relational-model)
  - [Structure](#structure)
  - [Manipulation](#manipulation)
  - [Integrity](#integrity)
  - [Data independence](#data-independence)
  - [Extensions](#extensions)
- [Functional relational programming](#functional-relational-programming)
  - [Architecture](#architecture)
  - [Benefits of this approach](#benefits-of-this-approach)
  - [Types](#types)

The biggest problem in the development and maintenance of large-scale software systems is complexity. The major contributor to this complexity is the handling of _state_. Other closely related are _code volume_, and explicit _flow of control_.

Object-oriented programming tightly couples state with related behaviour, and functional programming eschews state and side-effects all together.

## Complexity

In the ["No Silver Bullet" paper](http://worrydream.com/refs/Brooks-NoSilverBullet.pdf) Brooks identified four properties of software which make software hard: Complexity, Conformity, Changeability and Invisibility.

Complexity is _the_ root of the vast majority of problems with software today, like the ones about unreliability, late delivery or lack of security.

### Simplicity is hard

The type of complexity we are discussing in this paper is the one which makes large systems _hard to understand_. The one that causes huge resources in _creating and maintaining_ such systems. This type complexity has nothing to do with the complexity related with a _machine executing a program_.

## Approaches to understanding

* **Testing**: Attempting to understand the system from the outside with observations about how it behaves. Performed either by a human or by a machine.
* **Informal reasoning**: Understand the system by examining it from the inside.

Reasoning is the most important by far, mainly because there are limits to what can be achieved by testing, and because informal reasoning is _always_ used.

The key problem with testing is that tells you _nothing at all_ when it is given a different set of inputs.

> Testing can be used very effectively to show the presence of bugs but never to show their absence – Dijkstra

_Informal reasoning_ is limited in scope, imprecise and hence prone to error, as well as _formal reasoning, which is dependant upon the accuracy of specification. It may often be prudent to employ testing _and_ reasoning together.

Is because of the limitations of these approaches that _simplicity_ is vital.

## Causes of complexity

### Complexity caused by state

#### Impact of state in testing

State affects all types of testing. The common approach to testing a stateful system is to start up such that it is in some kind of "clean" or "initial" state, perform the desired tests upon the assumption that the system would perform in the same way every time the test is run. Sweeping the problem of state under the carpet.

It's not _always_ possible to "get away with it", some sequence of events can cause the system to "get into a bad _state_", then thing can go wrong.

Even though the number of _inputs_ may be very large, the number of possible _states_ the system can be is often even larger.

#### Impact of state in informal reasoning

The mental processes which are used to do this informal reasoning often revolve around a case-by-case mental simulation of behaviour. As the number of states grows, the effectiveness of this mental approach buckles quickly.

Another issue for informal reasoning is _contamination_.

Consider a system made up of procedures, some of which are stateful and others which aren't. If the procedure makes use of any procedure which _is_ stateful, _even indirectly_, the procedure becomes _contaminated_.

The more we can do to _limit_ and _manage_ state, the better.

### Complexity caused by control

Control is about _order_ in which things happen. We do not want to have to concerned about this.

When control is an implicit part of the language, every single piece of program must be understood in that context. When a programmer is forced to specify the control, he or she is being forced to specify an aspect of _how_ the system should work rather than simply _what_ is desired. They are being forced to _over-specify_ the problem.

A control-related problem is concurrency, which affects _testing_ as well.

Concurrency is normally specified _explicitly_ in most languages. The most common model is "shared-state concurrency" in which explicit synchronisation is provided. The difficulty for informal reasoning comes from adding further the _number of scenarios_ that must mentally be considered as the program is read.

Running a test in the presence of concurrency tells you _nothing at all_ about what will happen the next time you run that very same test.

### Complexity caused by code volume

This is a secondary effect. Much code is simply concerned with managing _state_ or specifying _control_. It is the easiest form of complexity to _measure_, and it interacts badly with the other causes of complexity.

Complexity definitively _does_ exhibit nonlinear increase with size (of the code) so it's vital to reduce the amount of code to an absolute minimum.

### Other causes of complexity

There are other causes like: duplicated code, dead code, unnecessary abstraction, missed abstraction, poor modularity, poor documentation...

All these come down to the following principles

* **Complexity breeds complexity**. Complexity introduced as a _result of_ not being able to clearly understand a system, like _Duplication_. This is particularly common in the presence of time pressures.
* **Simplicity is hard**. Simplicity can only be attained if it is recognised, sought and priced.
* **Power corrupts**. In the absence of language-enforced guarantees mistakes (and abuses) _will_ happen. We need to be very wary of any language that even _permits_ state, regardless of how much it discourages its use, the more _powerful_ a language, the harder it is to _understand_ systems constructed in it.

## Classical approaches to managing complexity

### Object-orientation

Imperative approach to programming.

#### State

An object is seen as consisting of some state together with a set of procedures for accessing and manipulating that state.

_Encapsulation_ allows the enforcement of integrity constraints over an object's state by regulating access to that state through access procedures ("methods").

One problem is that if several of the access procedures access or manipulate the same bit of state, then there may be several places where a given constraint must be enforced. Another major problem is that encapsulation-based integrity constraint enforcement is strongly biased toward single-object constraints, and it's awkward to enforce more complicated constraints involving multiple objects.

##### Identity and state

Each object is seen as being uniquely identifiable entity regardless of its attributes. This is known as _intentional_ identity (in contrast with _extensional_ identity in which things are considered the same if their attributes are the same).

Object identity _does_ make sense when objects are used to provide a (mutable) stateful abstraction.

However, where mutability is _not_ required, the OOP approach is the creation of "Value Objects". It is common to start using custom access procedures to determine whether two objects are equivalent. There is no guarantee that such domain-specific equivalence concepts conform to the standard idea of an equivalence relation (peg: no guarantee of transitivity).

The concept of _object identity_ adds complexity to the task of reasoning about systems developed in OOP.

##### State in OOP

All forms of OOP rely on state, and general behaviour is affected by this state. OOP does not provide an adequate foundation for avoiding complexity.

#### Control

Standard sequentual control flow and explicit classical "shared-state concurrency" cause standard complexity errors. A slight variation of "message-passing" Actor model canis not lead to easier informal reasoning but is not widespread.

#### Summary

Conventional imperative and object-oriented programs suffer greatly from both state-derived and control-derived complexity.

### Functional programming

It has its roots in the completely stateless lambda calculus of Church.

#### State

Functional programming languages are often classified as "pure" which shun state and side-effects completely, and "impure", whilst advocating the avoidance of state and side-effects in general, do permit their use.

By avoiding state (and side-effects) the entire system gains the property of _referential transparency_, a function will _always_ return exactly the same result. Because of this, testing does become far more effective.

By avoiding state, informal reasoning becomes much more effective.

#### Control

Functional languages do derive one slight benefit when it comes to control because they encourage a more abstract use of control functionals (such as `fold` / `map`) rather than explicit looping. There are also concurrent versions.

#### Kinds of state

By "state" what is really meant is _mutable state_.

Language which do not support or discourage mutable state it is common to achieve somewhat similar effects by means of passing extra parameters to procedures (functions).

There is no reason why the functional style of programming cannot be adopted in stateful languages. Whatever the language being used, there are large benefits to be had from avoiding, implicit, mutable state.

#### State and modularity

State permits a particular kind of modularity, within a stateful framework it is possible to add state to any component without adjusting the components which invoke it. Within a functional framework the same effect can only be achieved by adjusting every single component that invokes it to carry the additional information around.

In a functional approach you are forced to make changes to every part of the program that could be affected, in the stateful you are not.

In a functional program _you can always tell exactly what will control the outcome of a procedure_ simply by looking at the arguments supplied where it is invoked. In a stateful program you can never tell what will control the outcome, and _potentially_ have a look at every single piece of code in the _entire system_ to determine this information.

The trade-off is between _complexity_ and _simplicity_.

The main weakness of functional programming is that problem arise when the system to be built must maintain state of some kind.

#### Summary

Functional programming goes along way towards voiding the problems of state-derived complexity.

### Logic programming

Together with functional programming _declarative_ style of programming places emphasis on _what_ needs to be done rather than exactly _how_ to do it.

#### State

Logic programming makes no use of mutable state, and for this reason profits from the same advantages as functional programming.

#### Control

Operational commitment ot _process_ the program is the same order as it read textually (depth first). Particular ways of writing down can lead to non-termination, which leads inevitably to the standard difficulty for informal reasoning caused by control flow.

#### Summary

Despite the limitations it offers the ability to escape from the complexity caused by control.

## Accidents and essence

Brooks defined difficulties of "essence" as those inherent in the nature of software and classified the rest as "accidents".

* **Essential complexity** is inherent in the _users problem_.
* **Accidental complexity** is complexity with which the development team would not have to deal in the ideal world.

Any real development _will_ need to contend with _some_ accidental complexity.

Complexity itself is not inherent (or essential) property of software. Much complexity that we do see in existing software is not essential (to the problem). The goal of software engineering must be both to eliminate as much of accidental complexity as possible and to assist with the essential complexity part of it.

## Recommended general approach

Complexity could not be _possibly_ avoided even in the ideal world.

### Ideal world

In the ideal world we would not be concerned about performance. Even in the ideal world, we would need to start with a set of _informal requirements_ from the prospective users. We would ultimately need something to _happen_, and we are going to need some _formality_.We are going to need to derive formal requirements from the informal ones.

The next step is simply to _execute_ these formal requirements directly.

Effectively what we have just described is in fact the very _essence_ of _declarative programming_, specify _what_ you require, not _how_ it must be achieved.

#### State in the ideal world

The aim for state is to get rid of it hoping that most will be _accidental state_.

All data will be provided (_input_) or _derived_.

**Input data** Included in the informal requirements and as such is deemed _essential_.
* If the system may be required to refer to the data in the future then it is _essential state_.
* If there is no such possibility and the data is designed to have some side-effect, the data need not to be maintained at all.

**Essential derived data (immutable)** Data can always be re-derived, we do _not_ need to store it in the ideal world (accidental state).

**Essential derived data (mutable)** This can be excluded and hence corresponds to _accidental state_.

**Accidental derived data** State that is _derived_ but _not_ in the users' requirements is _accidental state_.

As a summary, mutable state can be avoided, even in the ideal world we _are_ going to have _some_ essential state.

_Accidental state_ can be excluded from the ideal world (by re-deriving the data as required). The vast majority of state isn't needed. One effect of this is that _all_ the state int he system is _visible_ to the user.

#### Control in the ideal world

Control generally can be completely omitted, so is considered _accidental_.

We should not have to worry about the control flow. _Results_ should be independent of the actual control mechanism. This is what logic programming taught us.

#### Summary

It is clear that a lot of complexity is _accidental_.

### Theoretical and practical limitations

#### Formal specification languages

_Executable specifications_ would be ideal. Declarative programming paradigm proposed approaches have been proposed as approaches for executable specifications.

In the ideal world, specifications derived _directly_ from the users' informal requirement is critical.

Formal specification has been categorised in two main camps:
* **Property-based** approaches focus on _what_ is required rather than _how_ the requirements should be achieved (_algebraic_ approaches such as Larch and OBJ).
* **Model-based (or state-based)** approaches construct a model and specify how that model must behave. These approaches specify how a stateful, imperative language solution must behave to satisfy the requirements.

There have been arguments against the concept of executable specifications. The main objection is that requiring a specification language to be executable can directly restrict its expresiveness.

In response, a requirement for this kind of expressivity does not seem to be common in many problem domains. Secondly where such specifications _do_ occur they should be maintained in their natural form but supplemented with a _separate_ operational component.

_Property-based_ approaches have the greatest similarity to _executable specifications_ in the ideal world.

A second problem is that even when specifications _are_ directly executable, this can be impractical for efficiency reasons. It may require some accidental components.

##### Ease of expression

Immutable, derived data would correspond to _accidental state_ and could be omitted (you could derive data on-demand).

There are occasionally situations where (using on-demand derivation) does not give rise to the most natural modelling of the problem.

An example of this is the derived data representing the position state of an opponent in an interactive game. It is at all times _derivable_ by a function of both all prior movements and the initial starting positions, but this is not the way it is most naturally expressed.

##### Required accidental complexity

* **Performance** making use of accidental state and control can be required for efficiency.
* **Ease of expression** making use of accidental state can be the most natural way to express logic in some cases.

#### Recommendations

_Avoid_ state and control where they are not absolutely and truly essential. When needed, such complexity must be _separated_ out from the rest of the system.

##### Required accidental complexity

* **Performance** _avoid_ explicit management of the accidental state, restrict ourselves to simply _declaring_ what accidental state should be used, and leave it to a completely separate infrastructure to maintain. We can effectively forget that the _accidental state_ even exists.
* **Ease of expression** this problem arises when derived (_accidental_) state offers the most natural way to express part of the logic of the system.

##### Separation and the relationship between components

First separate _all_ complexity of any kind from the pure logic (_logic_ / _state_ split).

Second, divide complexity between _accidental_ and _essential_. The essential bits correspond to the requirements.

"Separate" is basically advocating clean distinction between all three of these components. Additionally, it advocates for a split between the state and control components of the "Useful" Accidental Complexity, but this is less important.

It may be ideal to use _different languages_ for each. The weaker the language, the more simple it is to reason about.

Separation is important because it "restricts the power" of each of the components independently. It facilitates reasoning about them as a whole.

Recommended architecture (arrows show static references)

       ┌───────────────┬────────────────────┐
    ┌──│               │                    │
    │  │              ─┼─► Essential Logic  │
    │  │   Accidental  │                    │
    │  │   State and   │──────────┼─────────┤
    │  │    Control    │          ▼         │
    │  │              ─┼─► Essential State  │
    │  │               │                    │
    │  └───────────────┴──────────────────┬─┘
    │       Language and Infrastructure   │
    └─────────────────────────────────────┘

* **Essential state** This is the foundation of the system. It can _make no reference_ to _either_ of the other parts. Changes in either of the other specifications may never require changes to the specification of essential state.
* **Essential logic** This is referred as "business" logic, it's expressed, in terms of the state, what must be true. It does _not_ say anything about how. Changes to the essential state specification may require changes to the logic specification, and changes to the logic specification may require changes to the specification for accidental state and control. It should _make no reference_ to _any_ part of the accidental specification.
* **Accidental state and control** The least important of the system. Changes to it can _never_ affect the other specifications.

## The relational model

This has nothing _intrinsically_ to do with databases. Relational features as _structuring_ and _manipulating_ data, and maintaining _integrity_ and consistency of state, are applicable to state and data in any context.

Not only that, it does also allow clear separation between the logical and physical layers of the system (_data independence_).

### Structure

#### Relations

A relation is a homogeneous _set of records_, each one of them composed by a set of _attributes_.

Relations can be:
* **Base relations** stored directly
* **Derived relations** also known as _Views_, defined in terms of other relations.

A relation can be considered a _value_, and consider mutable state not as a "mutable relation" but rather a _variable_ which at any time can contain a particular relation _value_ (_relation variables_ or _relvars_).

#### Structuring benefits of relations, access path independence

Structuring data using relations is appealing because there is no need for up-front decisions need to be made about the _access paths_ to be queried later.

The ability of the relational model to _avoid_ access paths completely was one of the primary reasons for its success.

There are disturbing similarities between the data structuring approaches of OOP and XML.

### Manipulation

There are two different mechanisms for expressing the manipulation aspects of the relational model, the relational calculus and the relational algebra.

Relational algebra consists of the following operations:
* **Restrict** unary operation, select of a subset.
* **Project** unary operation, creates a new relation corresponding to the old relation.
* **Product** binary operation, cartesian product.
* **Union** binary operation, all records in either argument relation.
* **Intersection** binary operation, all records in both argument relations.
* **Difference** binary operation, all records in the first but no the second argument relation.
* **Join** binary operation, all possible records that result from matching identical attributes.
* **Divide** ternary operation, all records of the first argument which occur in the second argument associated with _each_ record of the third argument.

One significant benefit of this manipulation language is that it has the property of _closure_, all operations can be nested in arbitrary ways.

### Integrity

Simply by specifying in a purely declarative way a set of constraints must hold.

The most common types of constraint are _primary_ keys and _foreign_ keys.

DBMSs provide _imperative_ mechanisms such as triggers for maintaining integrity.

### Data independence

Is the principle of separating the logical model from the physical storage representation.

### Extensions

Relational algebra is a restrictive language in computational terms, and is normally augmented.

Common extensions include:
* **General computation capabilities** for example simple arithmetical operations.
* **Aggregate operators** `MAX`, `MIN`, `COUNT`, `SUM`, etc.
* **Grouping and summarisation capabilities**
* **Renaming capabilities**

## Functional relational programming

FRP is purely hypothetical, it has not in any way been proven in practice.

In FRP all _essential state_ takes the form of relations, and the _essential logic_ is expressed using relational algebra extended with (pure) user-defined functions.

The goal behind the FRP is the _elimination of complexity_.

The components of an FRP system.

    ┌───────────────┬────────────────────┬─────────┐
    │               │▒▒▒▒▒▒▒▒▒░░░░░░░░░░░│         │
    │               │▒ Essential Logic  ─┼─►       │
    │   Accidental  │▒▒▒▒▒▒▒▒▒░░░░░░░░░░░│         │
    │   State and   │────────────────────┤  Other  │
    │    Control    │░░░░░░░░░░░░░░░░░░░░│         │
    │               │░ Essential State ◄─┼─        │
    │               │░░░░░░░░░░░░░░░░░░░░│         │
    └───────────────┴────────────────────┴─────────┘

              ▒ Functional  ░ Relational

### Architecture

_Separate_ specifications for each of the following components:
* **Essential state** A relational definition of the stateful components of the system.
* **Essential logic** Derived-relation definitions, integrity constraints and (pure) functions.
* **Accidental state and control** A declarative specification of a set of performance optimisations for the system.
* **Other** Interfaces o the outside world.

In contrast with the object-oriented approach, FRP emphasises a clear _separation_ of state and behaviour.

#### Essential state ("state")

Essential state for the system in terms of base relvars (in FRP state store solely in terms of relations).

FRP strongly encourages data to be treated as essential state _only_ when it has been _input directly by a user_.

#### Essential logic ("behaviour")

Compromises both functional and algebraic relational parts.

The definitions can make use of an arbitrary set of pure user-defined functions.

Logic specifies a set of _integrity constraints_, boolean expressions which must hold at all times.

#### Accidental state and control ("performance")

Consists of a series of isolated performance "hints". They should be declarative in nature and intended to provide guidance to the infrastructure. It provides a means to specify _what state_ (accidental) should exist. amd it provides means to specify _what physical storage mechanisms_ should be used.

#### Other (interfacing)

Basically _interfacing with the outside world_.

All input must be converted into relational assignments (replace the old relvar values in the _essential state_ with new ones), and all output (and side-effects) must be driven from changes to the values of relvars.

There will probably be a requirement for a series of _feeder_ (or _input_) and _observer_ (or _output_) components.

These components will be of a _minimal_ nature, performing only the necessary translations to and from relations.

* **Feeders** convert input into relational assignments (causes changes to the _essential state_). _Feeders_ will need to specify them in some form of _state manipulation language_ provided by the infrastructure.
* **Observers** generate output in response to changes which they observe in the values of the (derived) relvars. At the minimum, they only need to specify the _name_ of the relvar which they wish to observe. Infrastructure will ensure that the observer is invoked. _Observers_ act both as _live-queries_ and also _triggers_.

#### Infrastructure

The FRP _system_ is the specification. _Infrastructure_ is what is needed to execute this specification. The requirements are:

**Infrastructure for essential state**
1. Store and retrieve data in the form of relations to named relvars.
2. A state manipulation language which allows the stored relvars to be updated.
3. Optionally secondary storage in addition to the primary one.
4. A base set of generally useful types.

**Infrastructure for essential logic**
1. Evaluates relational expressions.
2. Provides a base set of useful functions.
3. Language to allow specification of the user-defined functions in the FRP system.
4. Optionally a means of type inference.
5. Means to express and enforce integrity constraints.

**Infrastructure for accidental state and control**
1. Specify which _derived_ relvars should actually be stored. Along with the ability to store such relvars _and ensure_ they are _up-to-date at all times_.
2. _Flexible_ physical storage mechanisms to be used by a relvar.

**Infrastructure for feeders and observers**

For _feeders_ to be able to process relational assignment commands. It is useful to include the ability to accept commands which specify new relvar values in terms of their previous values (`INSERT`, `UPDATE`, `DELETE`) .

For _observers_ to be able to supply new value of a relvar whenever it changes. Extensions that could be useful are the ability to provide deltas, throttling and coalescing capabilities.

The ability to access arbitrary _historical_ relvar values would obviously be a useful extension in some scenarios too.

---

It is possible to develop an FRP infrastructure in _any_ general purpose language, object-oriented, functional or logic.

### Benefits of this approach

#### Benefits for state

It _avoids_ useless accidental state, and to avoid ever getting into a "bad state".

From the point of view of the logic, the _essential state_ is seen as a _constant_.

The _functional_ component (of the logic) has _no access_ to any state at all, it is referentially transparent.

There are major advantages from adopting relational representation of data such no concern with data access paths.

Finally, integrity of constraints provide big benefits for maintaining consistency of state in a _declarative_ manner.

#### Benefits of control

Control is _avoided_ completely. In FRP the logic consist simply of a set of equations with no intrinsic ordering or control flow at all.

An _infrastructure_ which supports FRP may well make use of _implicit_ parallelism to improve its performance.

It is also much easier to create distributed implementations.

#### Benefits of code volume

It _avoids_ useless accidental complexity and that leads to less code.

It reduces the harm that large volumes of code through its use of _separation_.

#### Benefits of data abstraction

Un-needed data abstraction actually represents another common cause of complexity via:
* **Subjectivity** Pre-existing data abstractions are too easily lead to _inappropriate_ reuse.
* **Data hiding** Erodes the benefits of referential transparency. Data which _does_ get used is _hidden_ at the function call site. This leads to problems for testing as well as informal reasoning in ways very similar to state.

One of the primary strengths of the relational model involves only minimal commitment to any subjective groupings.

#### Other benefits

Potential benefits include performance and development teams themselves could be organised around different components.

### Types

FRP provides a limited ability to define new user types for use in the _essential state_ and _essential logic_ components.

It _does not_ permit the creation of new product types, this is in order to _avoid_ any unnecessary data abstraction.