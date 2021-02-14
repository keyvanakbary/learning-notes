# [Programming Across Paradigms](https://www.youtube.com/watch?v=Pg3UeB-5FdA)

The paradigms of Programming, Robert W. Floyd Stanford University Turing Award Lecture

> I believe the chance we have to improve the general practice programming is to attend our paradigms – Robert W. Floyd

## What is a paradigm?

Philosophy, "The Structure of Scientific Revolutions". A paradigm is a worldview, how do we observe the universe, a model. A paradigm enables progress. **Unless we agree onto something is very difficult to progress as a community.**

> In learning a paradigm the scientists acquires theory, methods, and standards together, usually in an inextricable mixture – Tomas S. Kuhn

What entities make up the universe how they behave and interact. What makes up a program? Which problems are worth solving which solutions are legitimate. Which problems we need to define as programmers? Which programs are the good ones?

> All models are wrong – George E. P. Box

`paradigm -> anomaly -> crisis -> shift -> paradigm...`

Ptolomeo model on the universe (earth at the center) was superseeded with Copernicus model (sun at the center) which was superseeded by the Newton model, and then Albert Einstein, etc.

## Major paradigms?

### Imperative programming

**Follow my commands, in the order I give them. Remember state.**

_It's like a complex clock, you need lots of precision._

This paradigm requires so much precision that a single issue can bring the entire thing down.

### Object-Oriented programming

**Keep your state to yourself. Receive messages. Respond as you see fit.**

It is still imperative, but at least these are handled in smaller chunks. Objects have little pieces of state. Everything is about the messages and relationships between them.

_It's like biological stem cells in a body. A cell in a larger tissue. Every stell have their own organs and pieces. They have receptors in the membrane, receiving messages from the outside_


### Functional programing

The solution to the problem with rigidity of imperative programming.

**Mutable state is dangerous. Pure functions are safe. Data goes in, data comes out.**

_This is like a factory. Where we have like an assembly line were we transform materials into different stages until we get a car._

### Declarative programming

Functional programming falls under a broader umbrella called Declarative Programming.

**These are the facts. This is what I want. I don't care how you do it.**

_This is like a puzzle, a sudoku, where you have these rules about the game. It doesn't matter how you place numbers in it._

SQL is a declarative language. A subparadigm of declarative programing is Logic Programming and Prolog for example.

## What do they have in common?

It looks like there is massive rivalry between Object-Oriented Programming and Fucntional programming? Is there anything in common?

They are both trying to solve the rigidity and the complexity of imperative style programming. They try to tackle shared mutable state. Functional programming just removes the problem by making data immutable, OOP solved it creating small chunks of data.

> I'm sorry that I long ago coined the term "objects" for this topic because it gets many people to focus on the lesser idea. The big idea is "messaging" – Alan Kay

`thing.do(some, stuff)`

`thing` is the recipient

`do` is the message with `some` and `stuff` as arguments.


```python
buddy.is_friend_of('guy')

buddy.send('is_friend_of', 'guy')

buddy('is_friend_of', 'guy')
```

We can do this with closures instead of Classes so it becomes functional. So we will have the same behaviour than with OOP. Is it fuctional or object-oriented?  Depends on your worldview or mindset!

## Which paradigm is the best?

> All models are wrong **but some are useful** – George E. P. Box

Paradigms are useful in different ways. Newton model still works and Albert Einstein also works for other things.

> Each paradigm supports a set of concepts that makes it the best for a certain kind of problem – Peter Van Roy

Maybe we can match our problem with the best paradigm to solve it.

> We shouldn't ask if the model is **true**, but more on if the model is **illuminating and useful** – George E. P. Box

Maybe changing a paradigm will make our problem easier to solve.

## What can a paradigm teach me?

**Imperative programing**: Be explicit, understand the implementation. Forces you to think how to optimise these little details.

**Declarative programming**: Be abstract, understand the domain. To think in the big picture ideas, and not how to implement them. We can change the implementation but the big picture remains the same.

**Object Oriented Programming and Functional Programming**: Encapsulate and communicate. Sometimes we can take advantage of Object Oriented Programming to encapsualte behaviour.

**Functional Programming**: Specialise, transform data. Functional programming can make a convoluted situation an easy task to solve.

---

**No paradigm is best absolutely, each is best for a certain case.**

A set concepts that match very well with a set of problems.

> If the advancement of the general art of programming requires the continuing invention and elaboration of paradigms, advancement of the art of the individual programmer requires that they expand their repertory of paradigms – Robert W. Floyd

As individuals we need to get comfortable with as many paradigms as possible, to have more tools in our toolbox.

**Learn new paradadigms, try multi-paradigm languages.**

## What's the point?

Paradigms enable programming, as they paradigms enable scientific progress. Not only about the entities that defines the problems, but also the problems we can solve.

Don't fight your paradigm, embrace it. Be often to shift when anomalies arise. Attend to your paradigms.