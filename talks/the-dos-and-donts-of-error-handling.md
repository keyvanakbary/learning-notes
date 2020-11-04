# [The Do's and Don'ts of Error Handling](https://www.youtube.com/watch?v=TTM_b7EJg5E)

> A system is fault-tolerant if it continues working even if something is wrong

> Work like this is never finished, it's always in-progress

* Hardware can fail (relatively uncommon)
* Software can fail (common)

## Overview

* Fault-tolerance cannot be achieved using a single computer – it may fail
* We have to use several computers
    * Concurrency
    * Parallel programming
    * Distributed programming
    * Physics – time to propagate messages
    * Engineering
    * **Message passing is inevitable** – the basis of Object-Oriented Programming
* Programming languages should make this ~easy~ doable

We are never going to eliminate failure, systems will be inconsistent. We have to deal with it.

* How individual computers work is the smaller problem. How the system works as a whole is important.
* How the computers are interconnected and the protocols used between computers is the significant problem.
* We want the same way to program large and small scale systems.

Why do we have to program differently for local programs to communicate (memory) versus distributed systems (message bus)?

In Object-Oriented Programming, Alan Kay said that the big idea behind Object-Oriented Programming was "messaging"

## Erlang

* Derived from Smalltalk and Prolog (influenced by ideas from CSP)
* Unifies ideas on concurrent and functional programming
* Follows laws of physics (asynchronous messaging)
* Designed for programming fault-tolerant systems

Invented Erlang to solve a problem, not the language to find a problem to be solved with it.

Building fault-tolerant software boils down to detecting errors and doing something when errors are detected.

> We can't fix our own errors in the same way if I'm having a heart attack, I'll need someone to help me out

## Types of errors

* Errors that can be detected at compile time
* Errors that can be detected at run-time
* Errors that can be inferred
* Reproducible errors
* Non-reproducible errors

## Philosophy

* Find methods to prove Software correct at compile-time
* Assume software is incorrect and will fail at run-time then do something about it at run-time

## Evidence for software failure is all around us

Proving the self-consistency of small programs will not help. Testing a system will tell us that is self-consistent, not that it is correct.

## Conclusion

* Some small things can be proven to be self-consistent.
* Large assemblies of small things are possible to prove correct.

---

1980 - Erlang model of computation rejected. Shared memory systems ruled the world.
1985 - Ericsson started working on "a replacement of PLEX", started thinking about errors. "errors must be corrected somewhere else", "shared memory is evil", "pure message passing"
1986 - Erlang, unification of OO with FP
1998 - Several products in Erlang, Erlang gets banned and moved to Open Source
2004 - Erlang model of computation widely adopted in many different languages.

## Types of system

* Highly reliable (nuclear power plant control, air-traffic), satellite (very expensive if they fail)
* Reliable (driverless cars) (moderately expensive if they fail. Kills people if they fail)
* Reliable (annoys people if they fail), banks, telephone
* Dodgy (cross if they fail), Internet, HBO, Netflix
* Crap (very cross if they fail), free apps

Different technologies are used to build and validate the systems.

How can we make software that works reasonably well even if there are errors in the software? "Making reliable distributed systems in the presence of software errors" book by Joe Armstrong

## Requirements

* Concurrency
* Error encapsulation
* Fault detection
* Fault identification
* Code upgrade
* Stable storage

## The "method"

* Detect all errors
* If you can't do what you want to do try to do something simpler (relax requirements)
* Handle errors "remotely" (detect errors and ensure that the system is put into a safe state defined by an invariant)
* Identify the "Error Kernel" (the part that must be correct)

## Supervision trees

The node can be on different machine. Akka is "Erlang supervision for Java and Scala"

## It works

* Ericsson smart phone data setup
* WhatsApp
* CouchDB (CERN)
* Cisco (netconf)
* Spine2 (NHS - uk - riak (basho) replaces Oracle)
* RabbitMQ

---

## What is an error?

* An undesirable property of a program
* Something that crashes a program
* A deviation between desired and observed behaviour

## Who finds the error?

* The program (run-time) finds the error
    * Errors
        * Arithmetic errors: divide by zero, overflow, underflow, ...
        * Array bounds violated
        * System routine called with nonsense arguments
        * Null pointer
        * Switch option not provisioned
        * An incorrect value is observed
    * What can we do
        * Ignore it (no)
        * Try to fix it (no)
        * Crash immediately (yes)
            * Don't make matters worse
            * Assume somebody else will fix the problem (someone up in the supervision tree, this is like rebooting the system)
    * What should the programmer do when they don't know what to do?
        * Ignore it (no)
        * Log it (yes)
        * Try to fix it (possibly, but don't make maters worse)
        * Crash immediately (yes)
    * In sequential languages with single threads, crashing is not widely 
* The programmer finds the error
* The compiler finds the error

## What's the big deal about concurrency?

A sequential program when crashes it turns everything down (single thread).

When in a parallel program something crashes, the rest should keep working. There are linked process, if a process dies, these other processes are going to tell the process has died; these processes are going to get error messages.

## Why concurrency?

* Fault-tolerance is impossible with one computer
* Scalable is impossible with one computer (yes, you can scale things vertically up to a limit; up to the capacity of the computer)
* Security is very difficult with one computer (if the system gets compromised, everything gets compromised)
* I want one way to program not two ways. One for local systems, the other for distributed systems (rules out shared memory)
* The world is concurrent

## Detecting errors

### Where do errors come from

* Arithmetic errors
    * Silent **and deadly** errors, errors where the program does not crash but delivers an incorrect result
    * Noisy errors, errors which cause the program to crash
    * Very difficult to get right
        * The same answer in a single and double precision does not mean the answer is right
        * If it matters, you must prove every line containing arithmetic is correct
        * Real arithmetic is not associative
* Unexpected inputs
* Wrong values
    * Programs does not crash, but the values computed are incorrect or inaccurate
    * How do we know if a program/value is incorrect if we do not have a specification
    * Many programs have no specifications or specs that are so imprecise to be useless
    * The specification might be incorrect _and the tests and the program_
* Wrong assumptions about the environment
* Sequencing errors
* Concurrency errors
* Breaking laws of maths or physics

---

The programmer does not know what to do: CRASH

> I call this "let it crash"
> Somebody else will fix the error
> Needs concurrency and links

What do you do when you receive an error?

* Maintain an invariant
* Try to do something simpler

## Is that all?

What's a message?
* A program is a black box
* There are thousands of programming languages
* What language used is irrelevant
* The only important thing is what happens at the interface, their behaviour
* Two systems are the same if they obey observational equivalence

We shouldn't care about what happen inside these boxes, we just take care about the boundaries.

* Interaction between components involves message passing
* There are very few ways to describe messages (JSON, XML)
* There are very very few formal ways to describe the valid sequences of messages (= protocols) between components
    * We need a way to describe protocols. Protocols are contracts. Contracts assign blame. We need an architecture that describes what we see on the wire: the contract checker
        * How do we describe contracts?