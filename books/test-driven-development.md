# [Test-Driven Development: By Example](https://www.goodreads.com/book/show/387190.Test_Driven_Development)

- [TDD videos](#tdd-videos)
- [Preface](#preface)
- [Money session](#money-session)
- [Xunit session](#xunit-session)
- [Test-Driven Development Patterns](#test-driven-development-patterns)
- [Red bar patterns](#red-bar-patterns)
- [Red bar patterns](#red-bar-patterns-1)
- [Green bar patterns](#green-bar-patterns)
- [Design patterns](#design-patterns)
- [Refactoring](#refactoring)
- [Mastering TDD](#mastering-tdd)

## TDD videos

I skipped the TDD sessions in the book, _Money Pattern_ with Java and _implementing xUnit_ with Python, so the summary can focus on the learnings. Some interesting videos on TDD

- [TDD intro by Kent Beck](https://www.youtube.com/watch?v=VVSSga1Olt8)
- [Making making CoffeeScript by Kent Beck](https://www.youtube.com/watch?v=nIonZ6-4nuU)
- [The Three Laws of TDD by Uncle Bob](https://www.youtube.com/watch?v=qkblc5WRn-U)

## Preface

Two simple rules:
* Write new code only when you first have a failing automated test.
* Eliminate duplication

The technical implications of these two simple rules:
* Design organically
* Write your own tests
* Provide rapid response to small changes
* Design highly cohesive, loosely coupled components, just to make testing easy.

Order of programming tasks:
1. **Red**: Write a little test that doesn't work, perhaps doesn't even compiler
2. **Green**: Make the test work quickly, committing whatever sins necessary in the process
3. **Refactor**: Eliminate all the duplication created in just getting the test to work

Why would a programmer work in tiny little steps when their mind is capable of great soaring swoops of design? Courage.

### Courage

Test-driven development is a way of managing fear during programming, this-is-a-hard-problem-and-I-can't-see-the-end-from-the-beginning.

TDD isn't an absolute like Extreme Programming. TDD is an awareness of the gap between decision and feedback during programming, and techniques to control that gap.

There are certainly programming task that can't be driven solely by tests, like security software and concurrency.

> My goal is to write clean code that works. Imagining a programming world in which all code was this clear and direct, where there were no complicated solutions, only apparently complicated problems begging for careful thought. TDD is a practice that can help you lead yourself exactly that careful thought.

### Story time

TDD is a set of techniques any programmer can follow, that encourage simple designs and test suites that inspire confidence. *If you are a genius, you don't need these rules.* If you are dolt, the rules won't help.

Two rules:
* Write a failing automated test before you write any code.
* Remove duplication

## Money session

The rhythm of TDD:
1. Quickly add a test
2. Run all the tests and see the new one fail
3. Make a little change
4. Run all tests and see them all succeed
5. Refactor to remove duplication


#### Create a test
We don't start with objects, we start with tests.

When we write a test, we imagine the perfect interface for our operation. We are telling ourselves a store about how the operation will look from  the outside. Our story wont' always come true, but better to start from the best possible API and work backwards than to make things complicated, ugly and "realistic" from the get go.

You'll might end up with multiple compile errors from a single test. It's common to start from the following code when non of the code exists yet.

```java
public void testMultiplication() {
  Dollar five = new Dollar(5);

  five.times(2);

  assertEquals(10, five.amount);
}
```

We might need a constructor, but it doesn't have to do anything. We might need a stub implementation for methods.

**We'll do the least work possible just to get the test to compile.**

Once we solve compilation errors, we run the test and we watch it fail. Failure is progress. We've transformed a much broader problem to "make this test work and make the rest of the tests work", which is in fact a much simpler and much smaller scope for fear.

#### Make it pass

The goal right now is not to get the perfect answer, the goal is to pass the test.

#### Make it right

Dependency is the key problem in software development at all scales. If dependency is the problem, duplication is the symptom.

Objects are excellent for abstracting away the duplication of logic. Eliminating duplication in programs eliminates dependency. By eliminating duplication before we go on the next test, we maximize our chance of being able to get the next test running with one and only one change.


### Degenerate objects

The general TDD cycle

1. **Write a test.** You are writing a story. Invent the interface you wish you had. Include all the elements int he story that you imagine will be necessary to calculate the right answers.
2. **Make it run.** Quickly getting that bar green dominates everything else.
3. **Make it right.** Remove the duplication you have introduced to get to quick green. The goal is clean code that works.

Divide an conquer, solve the "that works" part, then solve the "clean code".

Strategies for quickly getting to green:
- **Fake it**, return a constant and gradually replace constants with variables until you have the real code.
- **Obvious implementation**, type in the real implementation.

When you know what to type, go for the obvious implementation. As soon as you get the unexpected red bar, back up and shift to fake implementation and refactor to the right code. Once confidence is back, go back to obvious implementation.

### Equality for all

There is a third strategy, **triangulation**. We briefly ignore the duplication between test and model code. When the second example demands a more general solution, then and only then do we generalize.

Use triangulation when you are completely unsure of how to refactor.

> Why would I need to write another test to give me permission to write what I probably could have written the first time?

Triangulation gives you a chance to think about the problem from slightly different direction. By varying the axes of variability to get a clearer answer.

### Privacy

From time to time, our reasoning will fail us and a defeat will slip through. When that happens, we learn our lesson about the test we should have written and move on.

### Equality for all, redux

When you don't have enough tests, you are bound to come across refactorings that aren't supported by tests. Write the tests you wish had. If you don't, you'll eventually break something while refactoring.

### Makin' objects

When you have two subclasses that aren't doing enough work to justify their existence and you want to eliminate them, you can't do it with one big step.

We could be a step closer eliminating the subclasses if there were fewer references to the subclasses directly. We could use Factory Method in the parent class to remove references to the subclasses in the tests.

By decoupling the tests from the existence of the subclasses, we have given ourselves freedom to change inheritance without affecting any model code.

### Time we're livin' in

Working in tiny steps is a recommendation, if it feels restrictive take bigger steps. If you feel unsure, take smaller steps. TDD is a steering process.

### Interesting times

We end up having clean code and tests that give us confidence that the clean code works. Rather than apply minutes of suspect reasoning, we can just ask the computer by making the change and running tests.

Without the tests you have no choice, you have to reason. With the tests you can decide whether an experiment would answer the question faster.

We'd prefer not to write a test when we have a red bar. We can't change model code without a test. The conservative course is back our the change that caused the red bar so we're back to green. Then we change the test, the implementation and re-try the original change.

### The root of all evil

When the object you have doesn't behave like you want, make another object with the same external protocol (an Imposter) but different implementation.

TDD can't guarantee that you will have flashes of insight at the right moment. However, confidence-giving tests and carefully factored code give you preparation for insight, and preparation for applying that insight when it comes.

### Change

No need for writing tests for `equals()` and `hashCode()` as we are writing those in the context of a refactoring.

### Abstraction, finally

For TDD to make economic sense, either you will have to be able to write twice as many lines per day as before, or write half as many lines for the same functionality. You'll have to measure and see effect TDD has on your own practice. Be sure to factor debugging, integrating, and explaining time into your metrics, though.

TDD can be used as a way to strive for perfection, but that isn't its most effective use. If you have a big system, the parts that you touch all the time should be absolutely rock solid, so you can make daily changes confidently.

### Retrospective

> I like running a code critic. Automated critics don't forget, if you don't delete an obsolete implementation, you don't have to stress. The critic will point it out.

The number of changes per refactoring should follow a "fat tail".

#### Test quality
Coverage is certainly not a sufficient measure of test quality, but it is a starting place. Another way of evaluating test quality is defect insertion. The idea is simple, change the meaning of a line of code and a test should break.

#### One last review

The three items that come up time and again as surprises when teaching TDD are
- The three approaches to making a test work cleanly: fake it, triangulate and just typing the right solution to begin with.
- Removing duplication between test and code as a way to drive the design.
- The ability to control the gap between tests to increase traction when the road gets slippery and cruise faster when conditions are clearer.


## Xunit session

### Invoke test method

Lots of refactoring has this feel, separating two parts so you can work on them separately. If they go back together when you are finished, fine, if not, you can leave them separate.

Another general pattern of refactoring, take code that works in one instance and generalize it to work in many by replacing constants with variables.

Starting from scratch is about the worst possible case for TDD, because we are trying to get over the bootstrap step. Once you mastered TDD, you will be able to work in much bigger leaps of functionality.

### Set the table

Patterns inside tests:
1. Arrange, create some objects.
2. Act, stimulate them.
3. Assert, check the results.

Two common constraints on tests come into conflict:
- *Performance*, we would like to run as quickly as possible and that might mean to share objects between tests.
- *Isolation*, we would like the success or failure of one test to be irrelevant to other tests.

One test can be simple if and only if another test is in place and running correctly. Simplicity of test writing is more important than performance.

### Cleaning up after

Doing a refactoring based on a couple of early uses, then having to undo it soon after is fairly common.

### Retrospective

The details of the implementation are not nearly as important as the test cases.

## Test-Driven Development Patterns

### Test _n_

No programmers release even the tiniest change without testing, except the very confident and the very sloppy.


Be careful with the positive feedback of not listening to stress and avoiding tests: The more stress you feel, the less testing you'll do. The less testing you do, the more errors you will make. The more errors you make, the more stress you feel.

With automated tests, when you start to feel stress, just run the tests. With automated tests you have a chance to choose your level of fear.

### Isolated test

**Make the tests so fast to run that you can run them yourself, and run them often. That way you can catch errors before anyone else sees them.**

Tests should be able to ignore each other completely. If you have one test broken, you want to have one problem. If you have two tests broken, you want to have two problems.

Isolating tests encourages you to compose solutions out of many highly cohesive, loosely coupled objects.

> I never knew exactly how to regularly achieve high cohesion and loose coupling until I started writing isolated tests.

### Test list

The first part of our strategy for dealing with programming stress is to never take a step forward unless we know where our foot is going to land.

What is it we intend to accomplish? One strategy for keeping track of what we're trying to accomplish is to hold it all in our heads.

> I tried this for several years, and found I got into a positive feedback loop. The more experience I accumulated, the more things I knew that might need to be done. The more things I knew might need to be done, the less attention I had for what I was doing. The less attention I had for what I was doing, the less I accomplished. The less I accomplished, the more things I knew that needed to be done.

Another strategy is to try to plan everything in advance and implement tests _en masse_.

Probably the best option is to always test first. Then we can get into a virtuous cycle: When we test first, we reduce the stress, which makes us more likely to test. The immediate payoff for testing, a design and scope control tool, suggests that we will be able to start doing it, and keep doing it even under moderate stress.

### Assert first

- Where should you start building a system? With stories you want to be able to tell about the finished system.
- Where should you start writing a bit of functionality? With the tests you want to pass with the finished code.
- Where should you start writing a test? With the asserts that will pass when it is done.

### Test data

Use data that makes the tests easy to read and follow. Don't have a list of 10 items as the input data if a list of 3 items will lead you the same design and implementation decisions.

The alternative to Test Data is Realistic Data, where you use data from the real world. Realistic Data is useful when:
- You are testing real-time systems using traces of external events
- You are matching the output of the current system with output of the previous system.
- You are refactoring a simulation and expect precisely the same answers when you are finished.

### Evident data

The intent of data should be represented  including expected and actual results in the test itself, trying to make their relationship apparent. Remember, you are writing the tests for the reader, not just the computer.

## Red bar patterns

If you don't find any test on the list that represents one step, add some new tests that would represent progress towards the items there.

### Starter test

The first question you have to ask with a new operation is "Where does it belong?"

Beginning with a realistic test will leave you too long without feedback. You can shorten the loop by choosing inputs and outputs that are trivially easy to discover.

### Explanation test
Ask for and give explanations in terms of tests.

### Another test

When a technical discussion is straying off topic with a tangential idea, add a test to the list and go back to the topic.

New ideas are greeted with respect, but not allowed to divert the attention. You write them down on the list and get back to what you were working on.

### Regression test

When a defect is reported write the smallest possible test that fails, and once it runs, the defect will be repaired.

### Break

When you feel tired or stuck take a break.

**Shower methodology**: if you know what to type, type. If you don't know what to type, take a shower.

TDD is a refinement of that strategy, if you don't know what to type, fake it. If the "right" design still isn't clear, triangulate. If you still don't know hat to type, then you can take that shower.

## Red bar patterns

- At the scale of a week, weekend commitments help get your conscious, energy-sucking thoughts off work.
- At the scale of a year, mandatory vacation policies help you refresh yourself completely.

### Do over

When you are feeling lost throw away the code and start over.

If you pair program, switching partners is a good way to motivate productive do overs.

### Child test

How do you get a test case running that turns out to be too big? Write a smaller test case that represents the broken part of the bigger test case.

### Mock object

In order to test an object that relies on an expensive or complicated resource, you create a fake version of the resource that answers constants.

Mock objects add a risk to the project, what if the mock doesn't behave like the real object? You can reduce this strategy by having a set of tests for the mock that can also be applied to the real object when it becomes available.

### Self Shunt

How do you test one object communicates correctly with another? Have the object under test communicate with the test case instead of the object it expects.

We don't need Spy objects.

```python
def testNotification(self):
    self.count = 0
    result = TestResult()
    result.addListener(self)
    WasRun("testMethod").run(result)
    assert 1 == self.count

def startTest(self):
  self.count = self.count + 1
```

Self Shunt tend to read better than tests written without.

### Log string

If you want to test that a sequence of messages are called correctly, keep a log in a string, and append to the string when a message is called.

Log strings are particularly useful when implementing Observer and you expect notifications to come at certain order. It works well with Self Shunt.

### Crash test dummy

If you want to test the flow for an error code, invoke a special object that throws an exception instead of doing real work.

### Broken test

How do you leave a programming session when you are programming alone? Leave the last test broken. When you come back to the code, you have an obvious, concrete bookmark to help you remember.

### Clean check-in

How do you leave a programming session when you are programming in a team? Leave all the tests running. When you are responsible to your teammates, the picture changes. You don't know in detail what has happened to the code since you saw it last. You need to start from a place of confidence and certainty.

## Green bar patterns

### Fake it ('til you make it)

The first implementation once you have a broken test should returning a constant. Once you have the test running, gradually transform the constant into an expression using variables. Having something running is better than not having something running.

Effects that make _fake it_ powerful:
- **Psychological**, having a green bar feels completely different than having a red bar.
- **Scope control**, Starting with one concrete example and generalizing from there prevents you from prematurely confusing yourself with extraneous concerns.

### Triangulate

How do you most conservatively drive abstraction with tests? Only abstract when you have two or more examples.

Once we have the two assertions and we have abstracted the correct implementation, we can delete one of the assertions on the grounds that it's completely redundant with the other.

> I only use triangulation when I'm really, really unsure about the correct abstraction for the calculation

### Obvious abstraction

Sometimes you know how to implement an operation. Go ahead.

Beware that solving "clean code" at the same time you solve "that works" can be too much to do at once.

### One to many

If you need to implement an operation that works with collection of objects, implement it first without collections and then make it work with them.

### Fixture

When you need objects needed by several tests, convert local variables in the tests into instance variables. Sometimes one fixture serves to test several classes.

### External fixtures

Release external resources in the `tearDown`. The goal of each test is to leave the world in exactly the same state as before it ran.

### Test method

All the tests sharing a single fixture will be methods in the same class. Tests requiring a different fixture will be in a different class.

The name of the method should suggest to a future clueless reader why this test was written.

> When I write tests, I first create a short outline of the tests I want to write like:
> // Adding to tuple spaces
> //// Taking a non-existing tuple
> // Taking from tuple to spaces

## Design patterns

The design patterns book seems to have a subtle bias towards design as a phase. It certainly makes no nod towards refactorign as a design activity.

### Command

When we need an invocation to be just a little more concrete and manipulable than a message, objects give us the answer. Make an object representing an invocation. Seed it with all the parameters the computation will need. When we're ready to invoke it, use generic protocol like `run()`. Lambda would work pretty well in this case.

### Value object

Objects are better than primitives because they are a great way to organize logic for later understanding and growth. However, there is one little problem.

**Aliasing problem**: If two objects share a reference to a third, if one object changes the referred object, the other object better not rely on the state of the shared object.

One solution is to never give out the objects that you rely on, but instead to always make copies.

Another solution is Observer, where you explicit register with objects on which you rely and expect to be notified when they change.

Another solution is to treat the object as less than an object and eliminate the "that change over time". Immutability and value is one of the core concepts of value objects. Every mutating operation just returns a new object. It makes reading and debugging so much easier.

All value objects have to implement equality.

### Null object

When you have a special case using objects, create an object representing the special case. Give it the same protocol as regular objects.

```java
SecurityManager security = SecurityManager.getSecurityManager();

if (security != null) {
    security.checkWrite(path);
}
```

to

```java
class LaxSecurity {
    public void checkWrite(String path) {
    }
}
class SecurityManager {
    public static SecurityManager getSecurityManager() {
        return security != null ? security : new LaxSecurity();
    }
}
```

Now we don't have to worry about someone forgetting to check for `null`.

```java
SecurityManager security = SecurityManager.getSecurityManager();

security.checkWrite(path);
```

### Template method

A way of representing invariant sequence of a computation while providing for future refinement is to write a method that is implemented entirely in terms of other methods.

A superclass can contain a method written entirely in terms of other methods, and subclasses can implement those methods in different ways.

Template methods are best found through experience instead of designed that way from the beginning.

### Pluggable object

The simplest way to express variation is with explicit conditionals

```java
if (circle) {

} else {

}
```

Such explicit decision making beings to spread.

```java
class SelectionTool {
    Figure selected;

    public void mouseDown() {
        selected = findFigure();
        if (selected != null)
            select(selected);
    }

    public void mouseMove() {
        if (selected != null)
            move(selected);
        else
            moveSelectionRectangle();
    }

    public void mouseUp() {
        if (selected == null)
            selectAll();
    }
}
```


The answer is to create Pluggable Object, a `SelectionMode` with two implementations `SingleSelection` and `MultipleSelection`.

```java
class SelectionTool {
    Figure selected;
    SelectionMode mode;

    public void mouseDown() {
        selected = findFigure();
        if (selected != null)
            mode = SingleSelection(selected);
        else
            mode = MultipleSelection();
    }

    public void mouseMove() {
        mode.mouseMove();
    }

    public void mouseUp() {
        mode.mouseUp();
    }
}
```

### Pluggable selector

If you want to invoke different behaviour for different instances, store the name of a method, and dynamically invoke it.

When you have ten subclasses of a class, each implementing only one method, subclassing is a heavyweight mechanism.

One alternative is to have a single class with a switch statement.

The Pluggable Selector solution is to dynamically invoke the method using reflection

```java
void print() {
    Method runMethod = getClass().getMethod(printMessage, null);
    runMethod.invoke(this, new Class[0]);
}
```

### Factory method

When you want to create an object wanting flexibility creating the new object, create the object in a method instead of using a constructor. Constructor slack expressiveness and flexibility.

By introducing a level of indirection, through a method, we gained the flexibility of returning an instance of a different class without changing the test.

The downside of Factory Method is precisely its indirection. You'll have to remember that the method is really creating an object. Use it when you need flexibility. Otherwise, constructors work just fine.

### Imposter

When you want to introduce a new variation into a computation, introduce a new object with the same protocol as an existing object but with different implementation.

Two examples of Imposters that come up frequently during refactoring:
- **Null Object**, treat the absence of data the same as the presence of data.
- **Composite**, treat a collection of objects the same as a single objects.

Finding Imposters during refactoring is driven by eliminating duplication.


### Collecting parameter

If you want to collect results spread over several objects, you add a parameter to the operation in which the results will be collected.

### Singleton

Avoid providing global variables through singletons, think about the design instead.

## Refactoring

Usually, refactoring cannot change the semantics of a program under any circumstances. In TDD, the circumstances we care about are the tests that are already passing. We can replace constants with variables in TDD and call this operation a refactoring because it doesn't change the set of tests to pass.

> _Leap of faith_ refactoring is exactly what we're trying to avoid with our strategy of small steps and concrete feedback.

## Mastering TDD

### What don't you have to test?

> Write tests until fear is transformed into boredom

Unless you have a reason to distrust it, don't test code from others.

### How do you know if you have good tests?

The tests are a canary in a coal mine revealing by their distress the presence of evil vapors. Signals that your design is in trouble.

- **Long setup code**. If you have to spend a hundred lines creating the objects for one simple assertion, something is wrong. Your objects are too big and need to be split.
- **Setup duplication**. If you can't easily find a common place for common setup code, there are too many objects too tightly intertwingled.
- **Long running tests**. TDD tests that run a long time won't be run often, and often haven't been run for a while, and probably don't work. Worse than this, this might suggest that testing the bits and pieces of the application is hard, and this is a design problem.
- **Fragile tests**. Tests that break unexpectedly suggest that one part of the application is surprisingly affecting another part.

### How does TDD lead to frameworks

Paradox: By not considering the future of your code you make your code much more likely to be able to adapt in the future.

### When should you delete tests?

Never delete a test if it reduces your confidence in the behavior of the system. If you have two tests that exercise the same path through the code, but they speak to different scenarios for readers, leave them alone.

If you have two tests that are redundant with respect to confidence and communication, delete the least useful of the two.

### How does the programming language and environment influence TDD?

In programming languages and environments where TDD cycles (test/compile/run/refactor) are harder to come by, you will be likely to be tempted to take larger steps.

### Can you drive development with application-level tests (ATDD)?

The problem with driving development with small scale test ("unit tests") is that you run the risk of implementing what you think a user wants.

If we wrote the tests at the level of the application, then the users could write tests themselves for what exactly they wanted the system to do next. There is a technical problem, how you can write and run a test for a feature that doesn't exist yet? There is a social problem with ATDD, writing tests is a new responsibility for users and organizations resist this kind of shift of responsibility.

TDD is a technique that is entirely under your control. Mixing up the rhythm of red/green/refactor, the technical issues of application fixturing, and the organizational change issues surrounding  user-written tests is unlikely to be successful. Another aspect of ATDD is the length of the cycle between test and feedback.

### How do you switch to TDD mid-stream?

The biggest problem is that code that isn't written with tests in mind typically isn't very testable. "Fix it", you say. Yes, well, but refactoring (without automated toos) is likely to result in errors, errors that you won't catch because you don't have the tests.

What you don't do is go write tests for the whole thing and refactor the whole thing, that would take months.

Parts of the system that don't demand change at the moment we will leave them alone.

We have to break the deadlock between tests and refactoring. We can get feedback working very carefully and with a partner. System level tests give us some confidence.

### Who is TDD intended for?

If you are happy slamming some code together that more or less works and never looking a the same result again, TDD is not for you. TDD rests on a charmingly naive geekoid assumption that if you write better code, you'll be more successful

What's naive is assuming that code is all there is to success. Good engineering is maybe 20% of a project's success. Bad engineering will certainly sink projects, but modest engineering can enable project success as long as the other 80% liens up for it.

Those whose souls are healed by the balm of elegance can find in TDD a way to do well by doing good. TDD is also good for geeks who form emotional attachments to code.

> My goal is to feel better about a project after a year than I did in the starry-eyed beginning, and TDD helps me achieve this.

### Why does TDD work?

Let's assume for the moment that TDD helps teams productively build loosely coupled, highly cohesive systems with low level defect rates and low cost of maintenance profiles. The sooner you find and fix a defect, the cheaper it is.

Programmers really do relax, teams really do develop trust, and customers really do learn to look forward to new releases.

It's effect is the way it shortens the feedback loop on design decisions.

> Adopt programming practices that "attract" correct code as a limit function, not as an absolute value.

### What's with the name?

One kind of the ironies of TDD is that it isn't a testing technique, it's an analysis technique, a design technique, really a technique for all the activities of development.

### Darach's challenge

- You can't test GUIs automaticaly
- You can't unit test distributed objects automaticaly
- You can't test-first develop your database schema
- There is no need to test third party code
- You can't test first develop a language compiler / interpreter.
