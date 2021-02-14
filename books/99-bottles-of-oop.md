# [99 Bottles of OOP](https://www.goodreads.com/book/show/31183020-99-bottles-of-oop)

- [Introduction](#introduction)
- [Rediscovering simplicity](#rediscovering-simplicity)
- [Test driving shameless green](#test-driving-shameless-green)
- [Unearthing concepts](#unearthing-concepts)
- [Practising horizontal refactoring](#practising-horizontal-refactoring)
- [Separating responsibilities](#separating-responsibilities)
- [Achieving openness](#achieving-openness)
- [Afterword](#afterword)

## Introduction

The book is about writing cost-effective, maintainable, and pleasing code.

Writing code is the _process_ of working your way to the next stable end point, not the end point itself.

## Rediscovering simplicity

You should not _reach_ for abstractions, but instead you should resist them until they absolutely insist upon being created.

### Simplifying code

The code should meet often contradictory goals. It must remain concrete enough to be understood while simultaneously being abstract enough to allow for change.

Code at the concrete end might be expressed as a single long procedure full of `if` statements. Code at the abstract end might consist of many classes, each with one method containing a single line of code.

The best solution for most problems lies not at the extreme of this continuum, but somewhere in the middle.

#### Incomprehensibly concise

##### Names

> **Terminology: Method versus Message**
> A "method" is defined on an object, and contains behaviour. An object like `Bottles` can define a method named `song`.
>
> A "message" is sent by an object to invoke behaviour. In the previous example, `song` can send the `verses` message to the implicit receiver `self`.
>
> Methods are _defined_, and messages are _sent_.
>
> The confusion between these terms comes about because it is common for the receiver of a message to define a method whose name exactly corresponds to that message. The `song` method sends the `verses` _message_ to `self`, which results in an invocation of the `verses` method.

Writing code is like writing a book; your efforts are for _other_ readers.

Getting insight into potential expense of a bit of code:

1. How difficult was it to write?
2. How hard is to understand?
3. How expensive will it be to change?


Code is easy to understand when it clearly reflects the problem it's solving, and thus openly exposes that problem's domain.

#### Concretely abstract

DRYing out code is not free. It adds a level of indirection, and layers of indirection make the _details_ of what's happening harder to understand. **DRY makes sense when it reduces the cost of change more than it increases the cost of understanding the code.**

You should name methods not after what they do (or how they behave), but after what they mean, what they represent in the context of your domain.

#### Shameless green (TDD)

The failure here is not bad intention, it's insufficient patience.

_Shameless Green_ is clearly the best solution, yet almost no one writes it. It feels embarrassingly easy, and is missing many qualities that you expect in good code.

One of the biggest challenges of design is when to stop, and deciding well requires making judgments about code.

### Judging code

#### Evaluating code based on opinion

Definitions generally describe how code looks when it's done without providing any concrete guidance about how to get there.

**Any pile of code can be made to _work_; good code not only works, but it also simple, understandable, expressive and changeable.**

#### Evaluating code based on facts

You can think of metrics as crowd-sourced opinions about quality of code.

##### Source lines of code (SLOC)

Measuring programmer productivity by counting lines of code assumes that all programmers write equally efficient code. Despite the fact that novices write more code to produce less function, by this metric, they can seem more productive.

SLOC numbers reflect code volume, and while it's useful for some purposes, knowing SLOC alone is not enough to predict code quality.

##### Cyclomatic complexity

A method with many deeply nested conditionals would score very high, while a method with no conditionals at all would score 0. You can use it to compare code or limit overall complexity. You can also use it to determine if you've written enough tests, as it tells you the minimum number of tests needed to cover all of the logic in the code.

##### Assignments, branches and conditions (ABC) metric

* _Assignments_ is a count of variable assignments.
* _Branches_ counts not branches of an if statement  but branches of control, meaning function calls or message sends.
* _Conditions_ counts conditional logic.

ABC scores are reflected as cognitive instead of physical size. It does measure complexity.

Metrics are fallible but human opinion is no more precise. Checking metrics regularly will keep you humble _and_ improve your code. Metrics clearly don't tell the whole story.

---

Infinitely experienced programmers do not write infinitely complex code; they write code that's blindingly simple.

The challenge comes when a change request arrives. Code that's good enough when nothing ever changes may _not_ be good enough when things do.

## Test driving shameless green

### Writing the first test

You can't figure out what's right until you write some tests. The purpose of some of your tests might very well be to prove that they represent bad ideas.

While it _is_ important to consider the problem and to sketch out an overall plan before writing the first test, don't overthink it.

Tests contain three parts:
* **Setup** Create the specific environment required for the test.
* **Do** Perform the action to be tested.
* **Verify** Confirm the result is as expected.

**As the tests get more specific, the code gets more generic.**

### Understanding transformations

In the ["Transformation Priority Premise"](https://8thlight.com/blog/uncle-bob/2013/05/27/TheTransformationPriorityPremise.html), Martin defines _transformations_ as "simple operations that change the behaviour of code".

Transformations are arranged in "priority" order, from simpler to more complex.

> 1. `({}–>nil)` no code at all->code that employs nil
> 2. `(nil->constant)`
> 3. `(constant->constant+)` a simple constant to a more complex constant
> 4. `(constant->scalar)` replacing a constant with a variable or an > argument
> 5. `(statement->statements)` adding more unconditional statements.
> 6. `(unconditional->if)` splitting the execution path
> 7. `(scalar->array)`
> 8. `(array->container)`
> 9. `(statement->recursion)`
> 10. `(if->while)`
> 11. `(expression->function)` replacing an expression with a function or algorithm
> 12. `(variable->assignment)` replacing the value of a variable.

### Tolerating duplication

As tests get more specific, code should become more generic. Code becomes more generic by becoming more abstract. One way to make code more abstract is to DRY it out.

**DRY is important but if applied to early, and with too much vigour, it can do more harm than good.** It's a good idea to ask the following questions when doing so:

* _Does the change I'm contemplating make the code harder to understand?_ Be suspicious of any change that muddies the waters.

* _What is the future cost of doing nothing now?_ Some changes cost the same regardless of whether you make them now or delay them until later. **If it doesn't increase your costs, delay making changes.**

* _When will the future arrive, or how soon will I get more information?_ It's better to tolerate duplication than to anticipate the wrong abstraction.

Writing Shameless Green means optimising for understandability, not changeability, and patiently tolerating duplication if doing so will help reveal the underlying abstraction.

### Exposing responsibilities

**Duplication is useful when it supplies independent, specific examples of a general concept that you don't yet understand.**

A specific method is responsible for understanding its input arguments, and for knowing how to use these arguments to produce the correct output. Responsibilities out of the scope of the method itself it should be delegated to other parts of the system.

When the obvious implementation is evident, it makes sense to jump straight to it. If you are absolutely certain of the correct implementation, there is no need to wear a hair shirt and repetitively inch through a series of tiny steps.

The small steps of TDD act to incrementally reveal the correct implementation. If your absolute certainty turns out to be wrong, **skipping these incremental steps means you miss the opportunity of being set right.**

Developing the habit of writing just enough code to pass the tests forces you to write better tests.

### Choosing names

Knowledge that one object has about another creates a dependency. Dependencies tie objects together, exacerbating the cost of change.


What's better to call `song` method, or to invoke `verses(0, 99)`?

```ruby
def song
  verses(0, 99)
end

def verses(starting, ending)
  #...
end
```

The `song` method imposes a single dependency. The `verses` method request the entire song, however requires significantly more knowledge:
* name of the method
* that it has two arguments: the first argument is the start, the second argument is the end
* the song starts on verse 99
* the song ends on verse 0

That's why `song` method is better from the client perspective.

### Writing cost-effective tests

The first step in learning the art of testing is to understand how to write tests that confirm _what_ your code does without the knowledge on _how_ your code does it.

### Avoiding the echo-chamber

Programmers who are hyper-alert to duplication, might be tempted to test `song` like this:

```ruby
def test_the_whole_song
  bottles = Bottles.new
  assert_equal bottles.verses(99, 0), bottles.song
end
```

This test has a major flaw that can cause it toggle from "short and sweet" to "painful and costly" in the blink of an eye. This flaw lies dormant until something changes, so the benefits of writing tests like this accrue to the writer today, while the costs are paid by an unfortunate maintainer in the future.

If you change an implementation detail while retaining existing behaviour and are then confronted with a sea of red, you are right to be exasperated. **This is completely avoidable, and a sign that tests are too tightly coupled to code. Such tests impede change and increase costs.**

There is a solution to this testing problem. The `song` test should know nothing about how the `Bottles` class produces the song. The clear and unambiguous expectation here is that song return the complete set of lyrics, and the best way and easies way to do it is to assert that it does:

```ruby
def test_the_whole_song
  expected = <<-SONG
ALL
# ...
THE
# ...
LYRICS
  SONG
  bottles = Bottles.new
  assert_equal expected, bottles.song
end
```

### Considering options

If you find the duplication distressing, consider the alternatives. Your choices are:

* _Assert that the expected output matches that of some other method._ Tests are coupled to the implementation, so these dependencies mean changes to the system under test might break the tests.

* _Assert that the expected output matches a dynamically generated string._ Reducing string duplication inside the test would f necessity require logic. Regardless of how you do it, any logic here means that a change to the system under test might break the test.

* _Assert that the expected output matches a hard-coded string._ Not only is the expected output clearly and unambiguously stated, but the test has no dependencies.

**Tests are not a place for abstractions, they are the place for concretions. Abstractions belong to the code.** If you insist in reducing duplication by adding logic to your tests, this logic by necessity must mirror the logic in your code. This binds the tests to implementation details and make them vulnerable to breaking every time you change the code.

---

Good tests not only tell a story, but they lead, step by step, to a well-organised solution.

## Unearthing concepts

### Listening to change

If the problem is solved, and you choose to refactor now rather than later, you pay the opportunity cost of not being able to work on _other_ problems. Spending time "improving" code based purely on aesthetics may bot be the best use of your precious time.

The need for change imposes higher standards on the affected code. **Code that never changes obviously doesn't need to be vary changeable, but once a new requirement arrives, the bar is raised.**

### Starting with the Open/Close Principle

The decision about whether to refactor in the first place should be determined by whether your code is already "open" to the new requirement.

**Code is open to a new requirement when you can meet the new requirement without changing existing code.**

The "open" principle says not conflate the process of refactoring, with the act of adding new features. **When faced with a new requirement, first rearrange the existing code such that it's open to the new feature, and once that's complete, then add the new code.**

### Recognising code smells

The trick to successfully improving code that contains many flaws is to isolate and correct them one at a time.

### Identifying the best point of attack

If you are unclear about how to make it open, the way forward is to start removing code smells.

### Refactoring systematically

> Refactoring is the process of changing a software system in such a way that it does not alter the external behaviour of the code yet improves its internal structure – Martin Fowler

You should never change tests during a refactoring. If your tests are flawed such that they interfere with refactoring, improve them first, and then refactor.

### Following the _Flocking Rules_

You can abstractions by iteratively applying a small set of simple rules (Flowing Rules):

1. Select the things that are most alike.
2. Find the smallest difference between them.
3. Make the simplest change that will remove the difference.

Changes to the code can be subdivided into four distinct steps:

1. Parse the new
2. Parse and execute it
3. Parse, execute and use its result
4. Delete unused code

### Converging on abstractions

#### Focusing on difference

DRYing out sameness has some value, but DRYing out difference has more.

If two concrete examples represent the same abstraction and they contain a difference, that difference must represent a smaller abstraction within the larger one.

#### Simplifying hard problems

It is common to find that hard problems are hard only because the easy ones have not yet been solved. Don't discount the value of solving easy problems.

#### Making methodical transformations

Making a slew of simultaneous changes is not refactoring, it's _rehacktoring_.

#### Refactoring gradually

Real refactoring is comfortingly predictable, and saves brainpower for more thought-provoking challenges.

## Practising horizontal refactoring

### Equivocating about names

Names should neither be too general nor too specific. When the perfect name for a concept is elusive, there are three strategies for moving forward:

* Dedicate five to ten minutes to ponder, and then use the best name that you can come up with.

* Instantly choose a meaningless name like `foo`. Like there is no point wasting time thinking about it now, the name will be obvious later.

* You can ask someone else for help.

### Deriving names from responsibilities

While you are allowed to use common sense, it's usually best to stay horizontal and concentrate on the current goal. The effort you put into selecting good names right now pays off by making it easier to recognise perfect names later.

### Seeking stable landing points

Code is read many more times than it is written, so anything that increases understandability lowers costs. Next, and just as important, consistent code enables _future_ refactorings.

### Obeying the Liskov Substitution Principle

The idea of reducing the number of dependencies imposed upon message senders by requiring that receiver return trustworthy objects is a generalisation of the Liskov Substitution Principle.

Liskov, in plain terms, requires that objects be what they promise they are. When using inheritance, you must be able to freely substitute an instance of a subclass for an instance of its superclass. Subclasses, by definition, are all their superclasses, _plus more_, so this substitution should always work.

Liskov Substitution Principle also applies to duck types. When relying on duck types, every object that asserts that it plays the duck's role must completely implement the duck's API. Duck types should be substitutable for one another.

Liskov violations force message senders to have knowledge of the various return types, and to either treat them differently or convert them into something consistent.

### Taking bigger steps

If you take bigger steps and the tests begin to fail, there's something about the problem that you don't understand. If this happens, don't push forward and refactor under red. Undo, return to green, and make incremental changes until you regain clarity.

### Depending on abstractions

Abstractions are beneficial in many ways. They consolidate code into a single place so that it can be changed with ease. They _name_ this consolidated code, allowing the name to be used as a shortcut for an idea, independent of its current implementation. These are valuable benefits, but abstractions also help in another, more subtle, way. In addition to the above, abstractions tell you where the code _relies_ upon an idea. But to get this last benefit, you must refer to an abstraction in every place where it applies.

## Separating responsibilities

### Selecting the target code smell

The truth about refactoring is that it sometimes makes things worse, in which case your efforts serve gallantly to disprove an idea.

#### Spotting common qualities

**Superfluous differences raises the cost of reading code, and increases the difficulty of future refactorings.**

Having multiple methods that take the same argument is a code smell. "Same" means _same concept_, not _identical name_. In an ideal world, each different concept would have its own unique, precise name, and there would be no ambiguity.

#### Enumerating flocked method commonalities

Conditionals could logically have used the less than greater than or not equal operations, and that would still have passed the tests.

Programmers tend to blithely interchange these different comparison operators, confident that if the tests pass, the code is correct.

**Testing for equality has several benefits over the alternatives. Most obviously, it narrows the range of things that meet the condition.** This reduces the difficulty of debugging errors. Testing of equality also makes the code more precise, and this precision enables future refactorings.

As an OO practitioner, when you see a conditional, the hairs on your neck should stand up. It means that objects are missing, and suggests that subsequent refactorigns are needed to reveal them.

This is not to say that you'll never have a conditional in an object-oriented application. **Collaborators must be brought together in useful combinations, and assembling these combinations requires knowing which objects are suitable.** Some object, somewhere, must choose which objects to create, and this often involves a conditional.

There is a big difference between a conditional that selects the correct object and one that supplies behaviour. The first is acceptable and generally unavoidable. The second suggests that you are missing objects in your domain.

### Extracting classes

_Primitive Obsession_ is when you use one of these data classes to represent a concept in your domain. Obsessing on a primitive results in code that passes built-in types around, and supplies behaviour for them.

The cure of _Primitive Obsession_ is to create new class to use in place of the primitive. For this operation, the refactoring recipe is _Extract Class_.

#### Modelling abstractions`

**It's easy to imagine creating objects that stand in for things, but the power of OO is that it lets you model ideas, things that don't physically exist.** Modellable ideas often lie dormant in interactions between objects.

Imagine an event management application, it might contain `Buyer` and `Ticket`, but also you place the logic for managing purchases, discounts or refunds into `Purchase`, `Refund` or `Discount` objects.

Experienced OO programmers deftly create virtual worlds in which ideas are as real as physical things.

#### Naming classes

**The rule about naming can thus be amended: while you should continue to name methods after what they _mean_, classes can be named after what they _are_.**

#### Extracting classes

You should refrain from altering the code of these copied methods until the new class is fully wired into the old.

#### Removing arguments

Learning the art of transforming code one line at a time, while keeping the tests passing at every point, let's you undertake enormous refactoring piecemeal.

#### Trusting the process

Refactorings that lead to errors can shake your faith in the validity of the corresponding recipes. However, these recipes have proven themselves reliable for many people across many circumstances. **If you adhere to a recipe and tests start failing, it's likely that there's something about the problem that you don't yet understand.**

### Appreciating immutability

The best things about immutable objects is that they are easy to understand and to reason about. These objects never start out one way and the secretly morph into something else.

Because they are easy to reason about, immutable objects are also easy to test. Tests for immutable objects avoid extra setup, which makes the tests cheaper to write and easier to understand.

Another key virtue of immutable objects is that they are thread safe. You can't break shared state if shared state doesn't change.

### Assuming _fast enough_

The benefits of immutability are so great that, _if it were free_, you'd choose it every time. Immutability's offsetting costs are twofold. First you must become reconciled of the idea, second achieving immutability requires the creation of more new objects.

The best programming strategy is to write the simplest code possible and measure its performance once you're done. If the whole is not acceptably fast, profile the performance, and speed up the slowest parts.

**Your goal is to optimise for easy of understanding while maintaining performance that's fast enough.** Don't sacrifice readability in advance of having solid performance data.

## Achieving openness

### Consolidating data clumps

_Data Clump_ is officially about _data_, and is defined as the situation in which several (three or more) data fields routinely occur together. Having a clump of data usually means you are missing a concept.

### Making sense of conditionals

**Instead of injecting an object and conditionally supplying it with behaviour, you should instead arrange code such that you can merely forward the message to the injected object.**

Fowler offers several curative refactoring recipes. The two main contenders are _Replace Conditional with State/Strategy_ and _Replace Conditional with Polymorphism_. _Polymorphism_ recipe uses inheritance, and _State/Strategy_ recipe does not.

Skilled programmers do what's right when they intuit the truth, but otherwise they engage in careful, precise, reproducible, and reversible coding experiments. **Practice builds intuition.**

### Replacing conditionals with polymorphism

Polymorphism allows senders to depend on the _message_ while remaining ignorant of the _type_, or class, of the receiver. Senders don't care what receivers are; instead, they depend on what receiver do.

#### Dismembering conditionals

Each conditional supplies _specific_ behaviour in its `true` branch and _generalised_ behaviour in its `false`.

Modern object-oriented programming is biased towards preferring composition over inheritance. However, this bias shouldn't be taken to mean that the use of inheritance is banned.

#### Manufacturing objects

The code that is said to "manufacture" an instance of the right kind of object is commonly referred as a _factory_.

**The factory's purpose is to isolate the names of the concrete classes, and to hide the logic needed to choose the correct one.**

Then you invoke the factory to get an object, you have no need to know the class of the returned object.

By refusing to be aware of the classes of the objects with which you interact, you grant others the freedom to alter your code's behaviour without editing its source. **Someone could amend the factory to return newly introduced players, and your existing code would happily collaborate with these unanticipated objects.**

#### Making peace with conditionals

Factories don't know _what_ to do: instead, they know how to choose who does. They consolidate the choosing and separate the chose.

You _can_ use polymorphism to create pluggable behaviour, and confine conditionals to factories whose job is to select the right object.

#### Transitioning between types

Correcting Liskov violations is important because object oriented programming, especially in dynamically-typed languages, relies on _explicit_ trust in the _implicit_ contracts between objects. Trustworthy objects are a joy to work with because they always behave as you expect.
Untrustworthy objects that sometimes fail to respond to a message force you into paranoid programming style. Untrustworthy objects require senders of messages to know too much.

When your application has code that needs knowledge of the internals of other objects in order to correctly interact them, changes to those other objects might break your code. **If you have to check the type of an object in order to know what message to send, you are forced into a conditional that lists every concrete class with which you're willing to collaborate. Doing this dooms you into changing the conditional when you add a new class.**

### Making the easy change

> Make the change easy (warning: this may be hard), then make the easy change – Kent Beck

Most of this book has been concerned with making the change easy. That hard work paid off, where you made the easy change.

### Prying open factory

Creating factories that are open for extension. If there is a predictable pattern to create needed objects, then it might be possible to dynamically generate the correct object for each case.

```ruby
class BottleNumber
  def self.for(number)
    begin
      const_get("BottleNumber#{number}")
    rescue NameError
      BottleNumber
    end.new(number)
  end
end
```

If you introduce a behaviour, there will be no need to change any existing code at all. Not even the factory, making the factory open too.

There are some reasonable objections:
1. This version is harder to understand than the original
2. Specific objects are no longer referenced in the source code. It will be hard to find references to the classes whose names are dynamically constructed.
3. The code uses an exception for flow control. Controlling the flow of a program with exceptions is roundly condemned.
4. The factory ignores bottle number classes whose names do not follow the convention.

## Afterword

Strive for simplicity. Don't abstract too soon. Focus on smells. Concentrate on difference. Take small steps. Follow the _Flocking Rules_. Refactor under green. Fix the easy problems first. Work horizontally. Seek stable landing points. Be disciplined. Don't chase the shiny thing.

In addition, deal with new requirements by first refactoring existing code to be open to them, and then writing new code to meet them. Achieving openness is usually the more challenging task, but can be sought in absolute safety if you have tests that act as a wall at your back.

Your job is not to be perfect, but to write a generous and sympathetic story.
