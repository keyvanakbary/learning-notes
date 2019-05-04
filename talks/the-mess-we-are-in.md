# [The Mess We Are In](https://www.youtube.com/watch?v=lKXe3HUG2l4)

- Broken images in Open-Office
- Slides on Keynote, async different versions not working
- Slides to PDF, requires Grunt. Grunt not found locally

* June 1948. Tom Kilburn, the first _modern_ programmer. 32bits.
* Year 1985. OS boots in 60 seconds.
* Typical laptop 2014. 1000x faster than previous generation. Should boot in 60ms, what happened?

Now we don't know why programs stop working, we used to know.
We are the job creators in the future.

## Seven deadly sins
1. Code even you cannot understand a week after you wrote it. **No comments**
  - We should write really big comments. A book!
2. Code with **no specifications**.
3. Code that is shipped as soon as it runs and before it is beautiful
4. Code with added features
5. Code that is very very fast very very **very obscure** and incorrect
6. Code that is **not beautiful**
7. Code that you wrote withut understanding the problem

## Legacy code
* Programmers who wrote the code are dead
* No specification
* Written in archaic languages which nobody understands
* "It works"
* Management thinks modifying legacy code is cheaper than a total re-write

---

* A program with 6 32bit integers can have more states than the number of atoms on the earth.
* Don't ask about Javascript.

A computer is a state machine. `State x Event -> New state`.

You need 2^7633587786 universes as the same number of atoms as states in my machine.

**We do never have the same state as other machines.**

## Failure

We have to deal with failure, we can't ignore it.

To handle  you need to understand. Computer 1 fails, Computer 2 detects this
* Distributed computing
* Parallel computing
* Concurrent programming

Systems should self-repair self-configure and evolve with time, like biological systems.

## Languages

Notation does not matter? Ask rommans to represent numbers!

In 1985 everybody* knew `sh`, `make`, `c`. Now programmers have no common language and cannot talk to each other.

Now we ahve 2500 languages to choose from. We don't have a lingua franca to communicate to each other.

Once upon a time all programmers understood `make`. Now we have `ant`, `grunt`, `make`, `rake`, `maven`, `jake`, `cake`, `bitcake`, `fabric`, `paper`, `shovel`, etc.

A program in Erlang with 3 modules and with bitcake downloaded and compile 46000. WTF.

Without Google and Stackoverflow programming would be impossible.

## Efficiency and clarity

To make something clearer add a layer of abstraction. To make something more efficient remove a layer of abstraction. Focus on clarity, speeds doubles every year.

## Names
* Names are imprecise
* Name imply a namespace
* The named thing might change
* Deciding a name is difficult
* Uniwue names are difficult to make

## What do the laws of physics say about computation

### Causality

* A cause must always precede its effect
* Information travels at or less than the speed of light
* We do not know that something has happened until we get a message saying that the event has happened
* We do not know how things are _now_ at a remote location only  how they were the last time we got a message from them

### Simultanuity

We have simultaneous observations about systems.

### Entropy always increases

If you throw a lot of dices in the air, they are not going to appear with a 6 up. They will be random. The more dices, the more entropy we have.

### Speed of computation

### Quantum mechanics fun

* Bremermann's limit
* Margolous-Levitin theorem
* The Bekenstein bound
* The Landauer Limit
* The Ultimate laptop
* The Ultimate computer

### The Ultimate laptop

The Ultimate laptop is a 1kg black hole...
* 10^51 ops sec
* Size 10^-27 meters
* Storage capacity 10^16 bits
* Lasts for 10^-21 seconds
* Emits data through Hawkings radiation and quantum entanglement

### The Ultimate computer

The ultimate computer is the entire universe
* 10^123 ops since it was booted
* Diameter 9.2x10^26 meters
* Storage capacity 10^92 bits
* Lasts for 10^10^1000

Reference: [Ultimate limits ultimate physical limits to computation - Seth Lloyd (MIT)](http://arxiv.org/abs/quant-ph/9908043)

## What can we do?

The entropy reverser. Entropy increses the number of files
All files -> The condenser -> Few files (break the 2nd law of thermodynamics)

* Files mutate
* Disk are huge
* What name should a file have
* Whic directory should I store the file in
* What machine should I store the directory in
* How will I find the file later
* How can I replicate the file

## URIs are bad

http://www.foo.se/a/b/c

* DNS can be spoofed
* The host can be unavailable
* If the story is changed the reference is wrong
* Can be cached (but for how long)
* Content can be changed by a person-in-the-middle

**Use hashes instead of names**

hash://367816778a768b6c45a4465e79798987f

* Address cannot be spoofed (there is no address)
* No problem choosing a name (there is no name)
* Can be cached (forever)
* Content can be validated on arrival
* No subject to person-in-the-middle attacks

How do you get the hash? Chrod Kademlia.

Ask the "nearest" machines to find stuff, which also have similar lists.

## How to make the condenser

1. Find all identical files
2. Merge all similar files. We need to find the most  similar file to a given file. If is a new idea, probably I should keep it. If not, maybe we can merge or reuse. `A similar B if size(C(A)) is similar to size(C(A++B))`

## Summary

* We've made a mess
* We need to reverse entropy
* Quantum mechanics sets limits to the ultimate speed of computation
* We need math
* Abolish names and places
* Build the condenser
* Make low-power computers, no net environmental damage

---

References
* [Programming Erlang](https://www.goodreads.com/book/show/38813666-programming-erlang)
* [Concurrent programming in Erlang](https://www.goodreads.com/book/show/808815.Concurrent_Programming_ERLANG)