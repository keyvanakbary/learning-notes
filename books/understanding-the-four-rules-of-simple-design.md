# [Understanding the Four Rules of Simple Design](https://www.goodreads.com/book/show/21841698-understanding-the-four-rules-of-simple-design)

- [Coderetreats](#coderetreats)
- [4 rules of simple design](#4-rules-of-simple-design)

The idea of "Good Design" can often lead to a feeling that there is a pinnacle. Prefer to talk about "Better Design".

The one constant that we know for sure in software development is that things are going to change.

Simple design, is one that is easy to change, the key to a "better design".

This does not mean that we should strive to make everything configurable. Quite the opposite. Rather than planning for change points, we build systems that can change at ANY point.

## Coderetreats

A day where you are encouraged to try new things. You don't have to live with the mistakes you've made during learning, you can just throw it away. It allows people to relax into the idea of not finishing.

Typically Coderetreats is about trying to solve the Conway's Game of Life automaton, deleting the code and changing the constraints by the hour.

## 4 rules of simple design

1. **Test pass.** If you can't verify that your system works, then it doesn't really matter how great your design is. This is about correctness and verification not automation specifically. When looking at your testing strategy, tend towards automated, and then towards making them fast(er).
2. **Express intent.** One of the most imporatnt qualities of a codebase, when it comes time to change, is how quickly you can find the part that should be changed. Paying attention to the names and how our code expresses itself.
3. **No duplication (DRY).** This is about _knowledge_ duplication (concepts). Instead of looking for code duplication, always ask yourself whether or not the duplication you see is an example of core knowledge in the system.
4. **Small.** It is important to look back and make sure that you don't have any extraneous pieces.
    * Is there any vestigial code that is no longer used
    * Are there any duplicate abstractions. Maybe there are abstractions with similar characteristics, missing another common abstraction that they can rely on.
    * Have we over-extracted. Once we do our cleanup, we can merge again extracted code.
  
---

An important thing to realise about these rules is that they iterate over each other.