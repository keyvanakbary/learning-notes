# [Simplicity is Complicated](https://www.youtube.com/watch?v=rFejpH_tAHM)


## Success

What makes Go successful?

* Speed of compilation
* Speed of execution
* Deployment
* Tools
* Libraries

Which are not language features, these are superficial reasons. All are important but not really the answer.

## Simplicity

Go is simple, at least compared to established languages. Simplicity has many facets. Simplicity is complicated.

## Convergence

Java, JavaScript, TypeScript, C#, C++, PHP actively borrow features from one another, they are converging into a single huge language.

## Language relativity

_Sapir-Whorf hypothesis_: Language influences thought.

Controversial with regard to human languages.

Close to a fact for computer languages. Consider:

* Logic programming
* Procedural programming
* Functional programming
* Object-oriented programming
* Concurrent programming

Like disciplines in mathematics. Like, you don't solve Calculus with Algebra even though they share semantics.

## Convergence and relativity

If the languages all converge, we will all think the same.

But different ways of thinking are good.

Need different languages for different problems.

We don't want just one tool, we want a set of tools, each best at one task.

## Convergence and features

Language evolve and compete by adding features.

The languages grow in complexity while becoming more similar.

Bloat without distinction.

## Features in Go

Go is different.

Go does not try to be like the other languages.

Go does not compete on features.

As of Go 1, the language is fixed.

Many newcomers to Go ask for features from other languages they know. But those features do not belong in Go, and the language is fixed.

Adding features to Go would not make it better, just bigger.

That would make Go less interesting by being less different.

## But you need features!

Of course, there must be _some_ features.

But which ones? The right ones!

Design by consensus.

## Readability

If a language has too many features, you waste time choosing which one to use. Then implement, refine, possibly rethink and redo.

Later, "Why does the code work this way?"

_The code is harder to understand simply because it is using a more complex language._

Preferable to have just one way, or at least fewer, simpler ways.

Features add complexity. We want simplicity.

Features hurt readability. We want readability.

Readability is paramount.

## Readable means reliable

Readable code is reliable code.

It's easier to understand.

It's easier to work on.

If it breaks, it's easier to fix.

If the language is complicated:
* You must understand more things to read and work on the code.
* You must understand more things to debug and fix it.

A key tradeoff: More fun to write, or less work to maintain? Go has been thought to make programs more maintainable in the long term.

## Expressiveness

Features are often suggested to aid "expressiveness".

Conciseness can be expressive but not always readable (imagine mathematical symbols).

Can also be expensive, implementing simple ideas with too-powerful primitives. Performance can also be unpredictable.

On the other hand, verbosity can inhibit readability by obscuring intent.

Build on, but do not be limited by, familiar ideas.

Be concise while remaining expressive.

## The right set of features

Not features for features' sake.

Features that "cover the space", like vector basis covering solution space.

Orthogonal features that interact predictably.

Simple features that interact in simple ways.

Simplicity comes from orthogonality and predictability.

Keep the language's goals in mind.

## Go's goals

Clean procedural language designed for scalable cloud software (infrastructure/ server infrastructure).

Composable distinct elements, including:
* Concrete data types
* Functions and methods
* Interfaces
* Packages
* Concurrency

Plus: Good tools, fast builds.

All the pieces feel simple in practice.

## Simplicity

Go is actually complex, but it _feels_ simple.

Interacting elements must mesh seamlessly, without surprises.

Requires a lot of design, implementation work, refinement.

Simplicity is the art of hiding complexity.

## A few simple things in Go

* Garbage collection
* Goroutines
* Constants
* Interfaces
* Packages

Each hides complexity behind a simple facade.

## Garbage collection

Perhaps the best example of simplicity hiding complexity.

Very difficult to implement well, but worth it.
Yet so simple the language specification mentions it only in the introduction.
Nonetheless, parts of the language strongly influenced by it.

Code is simpler because GC is there.
Design does not need to include "ownership".

Go: There is no `free`. There is only garbage collection.
As simple as it can be. (But complex behind the facade.)

## Concurrency

Concurrency is the ability to write your program as independently executing pieces. In Go, concurrency has three elements:
* goroutines (execution)
* channels (communication)
* `select` (coordination)

## Goroutines


Start a goroutine with the `go` keyword:

```go
go function(args)
```

Like garbage collection, eliminate considerations form the programmer's concern:
* no stack size
* no return or completion status
* no mechanism for management
* no "ID"

These are things other systems would provide. Go instead has a minimalist design.

Implementation complex, dependent on garbage collection for stack management.

## Constants

In Go, constants are just numbers, even though (because) it is strongly typed.

```go
var nanosecond = time.Second/ie9
```

Simple idea took about a year to work out. Difficulties:
* "infinite" precision integers
* "ifinite" precision floating point (tried and failed with rationals)
* promotion rules (`i := 2; f := 2.0; g := 1/2; h := 1/2.0`)
* corner cases like shift
  ```go
  fmt.Printf("%T %T", 2.0, 2.0<<0)
  ```

Still not totally satisfied, but the effect is that constants feel like numbers, contribute to ease of using Go. But complicated behind the scenes.

## Interfaces

Just a set of methods. No data. Simple idea, but more complex than expected

```go
type Reader interface {
    Read([]byte) (int, error)
}
```

Also need variables of that type (`var reader io.Reader`).
These variables add dynamic typing to a statically typed language.

```go
var r Reader = os.Stdin // statically checked.
var x interface{} = os.Stdin // statically checked.
r = x.(Reader) // dynamically checked. Must be explicit here, design decision.
```

Requires careful design. Interface assignment must be implemented at run time (not a v-table). What if it fails? Led to type assertions and the "comma, ok" idiom.

More complecity crept in. Type assertions and type switches were not in the original plan.

Go's most distintive and powerful feature.

Profound effect on library design.

Enables true component architectures. Prime examples are `io.Reader` and `io.Writer`, generalisations of the Unix pipe idea.

Feel simple, worth the complexity.

## Packages

A design for structuring programs and libraries.

```go
package big
...
import "math/big"
```

Took a long time to design. Enable componentisation, scalability, sharing, data hiding and isolation, ...

Affect program design, syntax, naming, building, linking, testing, ...

Separation of package path (`"math/big"`) from package name (`big`). Enabled the `go get` mechanism.

Intrincate to implement yet natural to use.

After garbage collection, perhaps the highest ratio of true complexity to apparent simplicity, and therefore of the power of simplicity to hide complexity.

## Summary

Simplicity is complicated but the clarity is worth the fight.

## Conclusion

Simplicity is hard – to design.

Simplicity is complicated – to build.

But if you get it right...

Simplicity is easy – to use.

The success of Go proves it.
