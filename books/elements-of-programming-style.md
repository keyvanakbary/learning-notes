# [The Elements of Programming Style](https://www.goodreads.com/book/show/454039.The_Elements_of_Programming_Style)

- [Introduction](#introduction)
- [Expression](#expression)
- [Control structure](#control-structure)
- [Program structure](#program-structure)
- [Input and output](#input-and-output)
- [Common blunders](#common-blunders)
- [Efficiency and instrumentation](#efficiency-and-instrumentation)
- [Documentation](#documentation)
- [Epilogue](#epilogue)

## Introduction

  * ### Write clearly, don't be too clever

    It is more important to make the purpose of the code unmistakable than to display virtuosity. The problem with obscure code is that debugging and modification become much more difficult, and these are already the hardest aspects of computer programming.

    Real programs are like prose.

    Although details vary from language to language, _the principles of style_ are the same. Branching around branches is confusing in any language.

    The job of critical reading doesn't end when you find a typo or even a poor coding practice.

    Don't treat computer output as gospel. If you learn to be wary of everyone else's programs, you will be better able to check your own.

## Expression

  * ### Say what you mean, simply and directly

    No amount of commenting, formatting, or supplementary documentation can entirely replace well expressed statements. After all, they determine what the program actually does.

  * ### Use library functions

    Library functions help to keep program size manageable, and they let you build on the work of others, instead of starting from scratch each time.

    Debugging is twice as hard as writing a program in the first place. So if you're as clever as you can be when you write it, how will you ever debug it?

  * ### Avoid temporary variables

    The fewer temporary variables in a program, the less chance there is that one will not be properly initialized, or that one will be altered unexpectedly before it is used.

  * ### Write clearly, don't sacrifice clarity for "efficiency"

    There is little justification for using the more obscure mode of expression. The harder it is for _people_ to grasp the intent of any given section, the longer it will be before the program becomes operational. Trying to outsmart a compiler defeats much of the purpose of using one.

  * ### Let the machine do the dirty work

    Repeated patterns of code catch the eye when scanning listings, why didn't the programmer let the computer do the repeating?

  * ### Replace repetitive expressions by calls to a common junction

  * ### Parenthesize to avoid ambiguity

  * ### Choose variable names that won't be confused

  * ### Avoid unnecessary branches
  
    One of the most productive ways to make a program easier to understand is to reduce the degree of interdependence between statements, so that each part can be studied and understood in relative isolation.

  * ### Use the good features of a language, avoid the bad ones

  * ### Don't use conditional branches as a substitute for a logical expression

---

The inversion and double parentheses slow comprehension. Example

```java
if (!(foo == false || bar == false)) {
  //...
}
```

Apply Morgan's rules

```java
!(A || B) == !A && !B
!(A && B) == !A || !B
```

---

  * ### Use the "telephone test" for readability

    If someone could understand your code when read aloud over the telephone, it's clear enough. If not, then it needs rewriting.

## Control structure

A computer program is shaped by its data representation and the statements that determine its flow of control. We will concentrate on matters of style that affect the program as a whole.

  * ### Use `IF-ELSE` to emphasize that only one of two actions is to be performed

    Be careful when tests might overlap.

    ```java
    if (hoursWorked <= 40)
      return registerPay();
    if (hoursWorked >= 40)
      return otherPay();
    ```

    An `IF-ELSE` ensures that someone reading the code can see that only one thing is done.

    ```java
    if (hoursWorked <= 40) {
      return registerPay();
    } else {
      return otherPay();
    }
    ```

  * ### Make your programs read from top to bottom

    It is a good rule of thumb that a program should read from top to bottom in the order that it will be executed.

  * ### Use `IF ... ELSE IF ... ELSE IF ... ELSE ..` to implement multi-way branches.

    ```java
    if (amountOfSales <= 50) {
      commission = 0;
    }
    if (amountOfSales > 50) {
      if (amountOfSales <= 100) {
        commission = 0.02 * amountOfSales;
      }
    }
    if (amountOfSales > 100) {
      commission = 0.03 * amountOfSales;
    }
    ```

    Better to write

    ```java
    if (amountOfSales <= 50) {
      commission = 0;
    } else if (amountOfSales <= 100) {
      commission = 0.02 * amountOfSales;
    } else {
      commission = 0.03 * amountOfSales;
    }
    ```

    When a program is well-structured, its layout can be made clean. Indentation is no substitute for organization; tasteful formatting and top-to-bottom flow is no guarantee that the code cannot be improved.
    As usual, no amount of commenting can rescue bad code.

  * ### Follow each decision as closely as possible with its associated action

    After you make a decision, do something. Don't just go somewhere or make another decision. If you follow each decision by the action that goes with it, you can see at a glance what each decision implies.

  * ### Use data arrays to avoid repetitive control sequences

  * ### Choose a data representation that makes the program simple

    Choosing a better data structure is often an art.

    > How can I organize the data so the computation becomes as easy as possible?

    Clarity is certainly not worth sacrificing just to save three tests per access.

  * ### Don't stop with your first draft

    No program is ever perfect; there is always room for improvement. It is foolish to polish a program beyond the point of diminishing returns, but most programmers do too little revision; they are satisfied too early.

## Program structure

Most programs are too big to be comprehended as a single chunk.

They must be divided into smaller pieces that can be conquered separately. Subroutines, functions, and procedures are the "modules," or building blocks, of large programs usable in other applications, contributing to a library of labor-saving routines.

When a program is not broken up into small enough pieces, the larger modules often fail to deliver on.

  * ### Modularize. Use subroutines

    It must be possible to describe the function performed by a module in the briefest of terms; and it is necessary to minimize whatever relationships exist with other modules, and display those that remain as explicitly as possible.

  * ### Make the coupling between modules visible

    If we wish to keep this as a separate module, the remaining shared data, should be explicitly passed as arguments.

  * ### Each module should do one thing well

    The print operation has nothing to do with the calculation; it merely happens to use the result. Combining too many functions in one module is a sure way to limit its usefulness, while at the same time making it more complex and harder to maintain.

  * ### Make sure every module hides something

    It is best to hide the details. inside a function that has a simple interface to the outside world. Exposing internal details increments general confusion and may well have to be changed later on.
    One good test of the worth of a module, in fact, is how good a job it does of hiding some aspect of the problem from the rest of the code.

    > A module should hide from its fellows the details of how it performs its task, for otherwise one module cannot be changed independently of others.

  * ### Let the data structure the program

    A big program should be a collection of manageable pieces, each of which must obey the rules of good style.

  * ### Don't patch bad code, rewrite it

    The fact that a four line comment is needed to explain what is going on should be reason enough to rewrite the code. Patching only serves to emphasize the shortcomings of this organization.

---
In a top-down design, we start with a very general pseudo-code statement of the program like

```
solve mazes
```

and then elaborate this statement in stages, filling in details until we ultimately reach executable code.

---

A powerful tool for reducing apparent complexity is recursion. In a recursive procedure, the method of solution is defined in terms of itself. The trick is to reduce each hard case to one that is handled simply elsewhere.

---

  * ### Write and test a big program in small pieces

    Once a program works, we need no longer concern ourselves with how it does something, only with the fact that it does. We thus have some assurance that we can deal with the program a small section at a time without much concern for the rest of the code.

  * ### Use recursive procedures for recursively-defined data structures

## Input and output

  * ### Test input for validity and plausibility

  * ### Make sure input cannot violate the limits of the program

  * ### Identify bad input, recover if possible

  * ### Make input easy to prepare and output self-explanatory

    Use of numeric codes is bad practice in a program that people use directly.

    The use of mnemonics like `RED` and `BLUE` instead of numeric codes like `1` and `2` is commendable, for it makes the program easier to use correctly. Use alphabetic names instead of numeric codes.

  * ### Use uniform input formats

  * ### Make input easy to proofread

  * ### Use free-form input when possible

    When there are many (i.e., more than one or two) arguments or parameters to be provided to a program, let the users specify their parameters by name.

    ```groovy
    method(feed: 27, diameter: 3.5, rpm: 3600)
    ```

    If input parameters are supplied by name, you can use default values in a graceful way.

  * ### Use self-identifying input. Allow defaults. Echo both on output

---

The hard part of programming is controlling complexity - keeping the pieces decoupled so they can be dealt with separately instead of all at once. And the need to separate into pieces is not some academically interesting point, but a practical necessity, to keep things from interacting with each other in unexpected ways.

Writing a separate input function is a prime example of decoupling.

---

  * ### Localize input and output in subroutines

    Input/output is the interface between a program and its environment. **Never trust any data, and remember the user.**

    Localize I/0 instead of spreading it all over the program. Hide the details of end of file, buffering, etc., in functions.

## Common blunders

A major concern of programming is making sure that a program can defend against bad data.

  * ### Make sure all variables are initialized before use

    You should still distinguish between true constants and initialized variables.

  * ### Don't stop at one bug

  * ### Watch out/or off-by-one errors

    A common cause of off-by-one errors is an incorrect test, for example using "greater than" when "greater than or equal to" is actually needed.

  * ### A void multiple exits from loops

  * ### Make sure your code "does nothing" gracefully

    Degenerate cases frequently arise where a piece of code has nothing to do - in this instance, when N is one or two, no search is necessary. In such cases it is important to "do nothing" gracefully; the `DO-WHILE` has this useful property.

  * ### Test programs at their boundary values

    Extra tests and branches add no safety factor. Quite the contrary, their existence makes the program that much harder to read and understand. The code will perform identically if the redundant tests are eliminated.

    One good strategy, both for writing and for testing, is to concentrate on the boundaries inherent in the program.

    The most obvious boundary in any program, and often the easiest to test, is what it does when presented with **no data at all**. The next boundary, also easy, is for **one data item**. And this time we see what is wrong.

  * ### Program defensively

    "Defensive programming" means anticipating problems in advance, and cod- ing to avoid errors before they arise.

    Another way to head off potential disasters is to "program defensively." Anticipate that in spite of good intentions and careful checking, things will sometimes go awry, and take some steps to catch errors before they propagate too far.

    At the cost of an occasional extra test and a little extra code, the program limits the spread of nonsense should anything damage the board.

    An important aspect of defensive programming is to be alert for these "impossible" conditions and to steer them in the safer direction.

  * ### 10.0 times 0.1 is hardly ever 1.0

    Floating point arithmetic adds a new spectrum of errors.

  * ### Don't compare floating point numbers just for equality

## Efficiency and instrumentation

Machines have become increasingly cheap compared to people. "Efficiency" involves the reduction of overall cost - not just machine time over the life of the program, but also time spent by the programmer and by the users of the program.

Efficiency does not have to be sacrificed in the interest of writing readable code - rather, writing readable code is often the only way to ensure efficient programs that are also easy to maintain and modify.

**Premature optimization is the root of all evil.**

  * ### Make it right before you make it faster

  * ### Keep it right when you make it faster

    Concern for efficiency should be tempered with some concern for the probable benefits, and the probable costs.

  * ### Make it clear before you make it faster

    Simplicity and clarity are often of more value than the microseconds possibly saved by clever coding.

  * ### Don't sacrifice clarity for small gains in "efficiency"

  * ### Let your compiler do the simple optimizations

  * ### Don't strain to re-use code, reorganize instead

  * ### Make sure special cases are truly special

    What did concern with "efficiency" in the original version produce, besides a bigger, slower, and more obscure program?

  * ### Keep it simple to make it faster

    Complexity loses out to simplicity. Fundamental improvements in performance are most often made by algorithm changes, not by tuning.

  * ### Don't diddle code to make it faster, find a better algorithm

    Time spent selecting a good algorithm is certain to pay larger dividends than time spent polishing an implementation of a poor method. For any given algorithm, polishing is not likely to significantly improve a fundamentally sound, clean implementation.

  * ### Instrument your programs. Measure before making "efficiency" changes

    The cost of computing hardware has steadily decreased; software cost has steadily increased. "Efficiency" should concentrate on reducing the expensive parts of computing.

## Documentation

The best documentation for a computer program is a clean structure. The only reliable documentation of a computer program is the code itself. Whenever there are multiple representations of a program, the chance for discrepancy exists. If the code is in error, artistic flowcharts and detailed comments are to no avail. Only by read- ing the code can the programmer know for sure what the program does.

This is not to say that programmers should never write documentation. It is vital to maintain readable descriptions of what each program is supposed to do, how it is used, how it interacts with other parts of the system, and on what principles it is based.

Anything that contributes no new information, but merely echoes the code, is superfluous.

A comment is of zero (or negative) value if it is wrong.

Code must largely document itself. If it cannot, rewrite the code rather than increase the supplementary documentation. Good code needs fewer comments than bad code does.

  * ### Make sure comments and code agree

    The trouble with comments that do not accurately reflect the code is that they may well be believed subconsciously, so the code itself is not examined critically.

  * ### Don't just echo the code with comments, make every comment count

  * ### Don't comment bad code, rewrite it

    A bad practice well commented remains bad. Variable names, labels can aid or hinder documentation.

  * ### Use variable names that mean something

  * ### Format a program to help the reader understand it

    The single most important formatting convention that you can follow is to indent your programs properly.

  * ### Indent to show the logical structure of a program

    If we eliminate the unnecessary grouping and nesting, things clarify remarkably.

    Unless we are consistent, you will not be able to count on what our formatting is trying to tell you about the programs. Good formatting is a part of good programming.

  * ### Document your data layouts

    One of the most effective ways to document a program is sim- ply to describe the data layout in detail. If you can specify for each important variable what values it can assume and how it gets changed, you have gone a long way to describing the program.

  * ### Don't over-comment

    We use few comments in our programs - most of the pro- grams are short enough to speak for themselves.

## Epilogue

Programmers have a strong tendency to underrate the importance of good style. Eternally optimistic, we all like to think that once we throw a piece of code together, however haphazardly, it will work properly the first time and ever after.

One excuse for writing an unintelligible program is that it is _a private matter_. It is the same justification you use for writing "qt milk, fish, big box" for a grocery list instead of composing a proper sentence. If the list is intended for someone else, of course, you had better specify what kind of fish you want and what should be inside that big box. But even if only you personally want to understand the message, if it is to be readable a year from now you must write a complete sentence. So in your diary you might write, "Today I went to the supermarket and bought a quart of milk, a pound of halibut, and a big box of raisins."
You learn to write as if to someone else because next year you will be "someone else."

**"Style" is not a list of rules so much as an approach and an attitude. "Good programmers" are those who already have learned a set of rules that ensures good style.**
