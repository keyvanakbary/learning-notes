# [Effective Java](https://www.goodreads.com/book/show/105099.Effective_Java_Programming_Language_Guide)

- [Creating and destroying objects](#creating-and-destroying-objects)
- [Methods common to all objects](#methods-common-to-all-objects)
- [Classes and interfaces](#classes-and-interfaces)
- [Generics](#generics)
- [Enums and annotations](#enums-and-annotations)
- [Lambdas and streams](#lambdas-and-streams)
- [Methods](#methods)
- [General programming](#general-programming)
- [Exceptions](#exceptions)
- [Concurrency](#concurrency)
- [Serialisation](#serialisation)

## Creating and destroying objects

### Consider static factory methods instead of constructors

```java
public static Boolean valueOf(boolean b) {
  return b ? Boolean.TRUE : Boolean.FALSE;
}
```

Advantages:
* They have names.
* They are not required to create a new object each time they are invoked.
* They can return an object of any subtype of their return type.
* The class of the returned object can vary from call to call as a function of the input parameters.
* The class of the returned object need to exist when the class containing the method is written.

Disadvantages:
* Classes that provide only static factory methods without public or protected constructors cannot be subclassed. This is preferable when using composition instead of inheritance.
* They are hard for programmers to find. Some conventions
  - `from`, as type-conversion method `Date d = Date.from(instant)`
  - `of`, an aggregation method `Set<Rank> faceCards = EnumSet.of(JACK, QUEEN, KING)`
  - `valueOf`, more verbose alternative than `from` and `of`, `BigInteger prime = BigInteger.valueOf(Integer.MAX_VALUE)`
  - `instance` or `getInstance`, returns and instance that cannot be said to have the same values, `StackWalker luke = StackWalker.getInstance(options)`
  - `create` or `newInstance` the method guarantees each call returns a new instance, `Object newArray = Array.newInstance(classObject, arrayLength)`
  - `get`**Type**, like `getInstance`but when factory method is in a different class `FileStore fs = Files.getFileStore(path)`
  - `new`**Type**, like `newInstance` but when factory method is in a different class `BufferedReader br = Files.newBufferedReader(path)`
  - **type**, a concise alternative to `get`_Type_ and `new`_Type_, `List<Compliant> litany = Collections.list(legacyLitany)`

### Consider builder when faced with many constructor parameters

```java
public class NutritionFacts {
    private final int servingSize;  // (mL)            required
    private final int servings;     // (per container) required
    private final int calories;     // (per serving)   optional
    private final int fat;          // (g/serving)     optional
    private final int sodium;       // (mg/serving)    optional
    private final int carbohydrate; // (g/serving)     optional

    public NutritionFacts(int servingSize, int servings) {
        this(servingSize, servings, 0);
    }

    public NutritionFacts(int servingSize, int servings, int calories) {
        this(servingSize, servings, calories, 0);
    }

    public NutritionFacts(int servingSize, int servings, int calories, int fat) {
        this(servingSize, servings, calories, fat, 0);
    }

    public NutritionFacts(int servingSize, int servings, int calories, int fat, int sodium) {
        this(servingSize, servings, calories, fat, sodium, 0);
    }

    public NutritionFacts(int servingSize, int servings, int calories, int fat, int sodium, int carbohydrate) {
        this.servingSize  = servingSize;
        this.servings     = servings;
        this.calories     = calories;
        this.fat          = fat;
        this.sodium       = sodium;
        this.carbohydrate = carbohydrate;
    }
}
```

The telescoping constructor pattern works, but it is hard to write client code when there are many parameters, and harder still to read it.

Avoid using JavaBeans pattern as it might leave the object in an inconsistent state partway through its construction. It does also precludes the possibility of making the class immutable.

```java
public class NutritionFacts {
    private final int servingSize;
    private final int servings;
    private final int calories;
    private final int fat;
    private final int sodium;
    private final int carbohydrate;

    public static class Builder {
        private final int servingSize;
        private final int servings;

        private int calories      = 0;
        private int fat           = 0;
        private int sodium        = 0;
        private int carbohydrate  = 0;

        public Builder(int servingSize, int servings) {
            this.servingSize = servingSize;
            this.servings    = servings;
        }

        public Builder calories(int val)
            { calories = val;      return this; }
        public Builder fat(int val)
            { fat = val;           return this; }
        public Builder sodium(int val)
            { sodium = val;        return this; }
        public Builder carbohydrate(int val)
            { carbohydrate = val;  return this; }

        public NutritionFacts build() {
            return new NutritionFacts(this);
        }
    }

    private NutritionFacts(Builder builder) {
        servingSize  = builder.servingSize;
        servings     = builder.servings;
        calories     = builder.calories;
        fat          = builder.fat;
        sodium       = builder.sodium;
        carbohydrate = builder.carbohydrate;
    }
}
```

```java
NutritionFacts cocaCola = new NutritionFacts.Builder(240, 8)
    .calories(100).sodium(35).carbohydrate(27).build();
```

The Builder pattern simulates named optional parameters and it is well suited to class hierarchies. **It is good choice when designing classes whose constructors or static factories would have more than a handful of parameters.**

### Enforce the singleton property with a private constructor or an enum type

Beware that making a class a singleton can make it difficult to test its clients because it's impossible to substitute a mock implementation /

**Singleton with public final field**, this approach is simpler and it makes it clear that the class is a singleton.

```java
public class Elvis {
    public static final Elvis INSTANCE = new Elvis();
    private Elvis() { ... }

    public void leaveTheBuilding() { ... }
}
```

**Singleton with static factory**

```java
public class Elvis {
    private static final Elvis INSTANCE = new Elvis();
    private Elvis() { ... }
    public static Elvis getInstance() { return INSTANCE; }

    public void leaveTheBuilding() { ... }
}
```

**Enum singleton**, similar to public field approach but more concise. It provides serialisation machinery for free and provides guarantee against multiple instantiation even on serialisation and reflection attacks. **This is the best way of implementing a singleton.**

```java
public enum Elvis {
    INSTANCE;

    public void leaveTheBuilding() { ... }
}
```

### Enforce noninstantiability with a private constructor

Ocassionally you'll want to write a class that is a grouping of static methods. People abuse them in order to avoid thinking in terms of objects, but they have valud use cases.

Such _utility clases_ are not designed to be instantiated.

Attempting to enforce noninstantiability by making the class abstract does not work. **A class can be made noninstantiable by including a private constructor.**

```java
public class UtilityClass {
    // Suppress default constructor for noninstantiability
    private UtilityClass() {
        throw new AssertionError();
    }
    // Remainder omitted
}
```

### Prefer dependency injection to hardwiring resources

Innapropiate use of static utility, inflexible and untestable.

```java
public class SpellChecker {
    private static final Lexicon dictionary = ...;

    private SpellChecker() {} // Noninstantiable

    public static boolean isValid(String word) { ... }
    public static List<String> suggestions(String typo) { ... }
}
```

Dependency injection provides flexibility and testability

```java
public class SpellChecker {
    private final Lexicon dictionary;

    public SpellChecker(Lexicon dictionary) {
        this.dictionary = Objects.requireNonNull(dictionary);
    }

    public boolean isValid(String word) { ... }
    public List<String> suggestions(String typo) { ... }
}
```

A useful variant of the pattern is to pass a resource _factory_ to the constructor so the object can be called repeatedly to create instance of a type.

```java
Mosaic create(Supplier<? extends Tile> tileFactory) { ... }
```

### Avoid creating unnecessary objects

```java
String s = new String("bikini");
```

Performance can be greatly improved

```java
static boolean isRomanNumeral(String s) {
    return s.matches("^(?=.)M*(C[MD]|D?C{0,3})"
        + "(X[CL]|L?X{0,3})(I[XV]|V?I{0,3})$");
}
```

Reusing expensive object for improved performance

```java
public class RomanNumerals {
    private static final Pattern ROMAN = Pattern.compile(
        "^(?=.)M*(C[MD]|D?C{0,3})" +
        "(X[CL]|L?X{0,3})(I[XV]|V?I{0,3})$");

    static boolean isRomanNumeral(String s) {
        return ROMAN.matcher(s).matches();
    }
}
```

Be careful with autoboxing, as it blurs the distinction betwen primitive and boxed primitive types. The following code is hideously slow, can you spot object creation?

```java
private static long sum() {
    Long sum = 0L;
    for (long i = 0; i <= Integer.MAX_VALUE; i++)
        sum += i;

    return sum;
}
```

Prefer primitives to boxed primitives, and watch out for unintentional autoboxing.

### Eliminate obsolete object references

Can you find the _memory leak_?

```java
public class Stack {
    private Object[] elements;
    private int size = 0;
    private static final int DEFAULT_INITIAL_CAPACITY = 16;

    public Stack() {
        elements = new Object[DEFAULT_INITIAL_CAPACITY];
    }

    public void push(Object e) {
        ensureCapacity();
        elements[size++] = e;
    }

    public Object pop() {
        if (size == 0)
            throw new EmptyStackException();
        return elements[--size];
    }

    /**
     * Ensure space for at least one more element, roughly
     * doubling the capacity each time the array needs to grow.
     */
    private void ensureCapacity() {
        if (elements.length == size)
            elements = Arrays.copyOf(elements, 2 * size + 1);
    }
}
```

Don't forget to null out references once they become obsolete!

```java
public Object pop() {
    if (size == 0)
        throw new EmptyStackException();

    Object result = elements[--size];
    elements[size] = null; // Eliminate obsolete reference
    return result;

}
```

Be mindful about this, **nulling out object references should be the exception rather than the norm.** The best way to eliminate an obsolete reference is to let the variable that contained the reference fall out of scope.

Whenever a class manages its own memory, the programmer should be alert for memory leaks.

Common sources of memory leaks are caches, listeners and callbacks.

### Avoid finalisers and cleaners

Finalisers are unpredictable, often dangerous, and generally unnecessary. Cleaners are less dangerous than finalisers, but still unpredictable, slow, and generally unnecessary.

Never do anything time-critical in a finalisers or cleaners. There is no guarantee they'll be executed promptly.

Never depend on a finaliser or cleaner to update persistent state. The language specification provides no guarantee that finalisers or cleaners will run at all.

There is a sever performance penalty for using finalisers and cleaners.

Finalisers have a serious security problem: they open your class up to finaliser attacks. Throwing an exception from a constructor should be sufficient to prevent an object form coming into existence; in the presence of finalisers, it is not. To protect nonfinal classes from finaliser attacks, write a final `finalize` method that does nothing.

Instead of writing a finaliser or cleaner, just have your class implement `AutoCloseable`.

### Prefer `try`-with-resources to `try-finally`

`try-finally` is no longer the best way to close resources.

```java
static String firstLineOfFile(String path) throws IOException {
    BufferedReader br = new BufferedReader(new FileReader(path));
    try {
        return br.readLine();
    } finally {
        br.close();
    }
}
```

`try-finally` is ugly when used with more than one resource.

```java
static void copy(String src, String dst) throws IOException {
    InputStream in = new FileInputStream(src);
    try {
        OutputStream out = new FileOutputStream(dst);
        try {
            byte[] buf = new byte[BUFFER_SIZE];
            int n;
            while ((n = in.read(buf)) >= 0)
                out.write(buf, 0, n);
        } finally {
            out.close();
        }
    } finally {
        in.close();
    }
}
```

`try`-with-resources is the best way to close resources.

```
static String firstLineOfFile(String path) throws IOException {
    try (BufferedReader br = new BufferedReader(new FileReader(path))) {
       return br.readLine();
    }
}
```

`try`-with-resources on multiple resources, short and sweet.

```
static void copy(String src, String dst) throws IOException {
    try (InputStream   in = new FileInputStream(src);
         OutputStream out = new FileOutputStream(dst)) {
        byte[] buf = new byte[BUFFER_SIZE];
        int n;
        while ((n = in.read(buf)) >= 0)
            out.write(buf, 0, n);
    }
}
```

## Methods common to all objects

### Obey the general contract when overriding `equals`

* Each instance of the class is inherently unique
* there is no need for the class to provide a "logical equality" test
* A superclass has overriden `equals`, and the superclass behaviour is appropiate for this class
* The class is private or package-private, and you are certain that its `equals` method will never be invoked.

`equals` method implements _equivalence relation_ for any non-null reference values:
* **Reflexive**: `x.equals(x)` must return `true`
* **Symmetric**:  `x.equals(y)` returns `true` if `y.equals(x)` returns `true`
* **Transitive**:  `x.equals(y)` returns `true` and `y.equals(z)` returns `true`, then `x.equals(z)` must return `true`
* **Consistent**:  `x.equals(y)` should consistently return `true` or consistently return `false`
* `x.equals(null)` must return `false`

Do not write an `equals` method that depends on unreliable resources.

All objects objects must be unequal to `null`.

A few more caveats:
* Always override `hashCode` when you override `equals`.
* Don't try to be too clever
* Don't substitute another type for `Object` in the `equals` declaration.

### Always override `hashCode` when you override equals

Equal objects must have equal hash codes.

Do not be tempted to exclude significant fields from the hash code computation to improve performance.

Don't provide a detailed specification for the value returned by `hashCode`, so clients can't reasonably depend on it; this gives you the flexibility to change it.

### Always override `toString`

Providing a good `toString` implementation makes your class much more pleasant to use and makes systems using the class easier to debug.

When practical, the `toString` method should return all the interesting information in the object.

Whether or not you decide to specify the format, you should clearly document your intentions.

### Override `clone` judiciously

In practice, a class implementing `Cloneable` is expected to provide a properly functioning public `clone` method.

Immutable classes should never provide a `clone` method, because that would only encourage wasteful copying.

The `clone` method functions as a constructor; you must ensure that it does no harm to the original object and that it properly establishes invariants on the clone.

The `Cloneable` architecture is incompatible with normal use of final fields referring to mutable objects.

Public `clone` methods should omit the `throws` clause, as methods that don't throw checked exceptions are easier to use.

A better approach to object copying is to provide a copy constructor or copy factory.

```java
public Yum(Yum yum) { ... }
```

```java
public static Yum newInstance(Yum yum) { ... };
```

Advantages of using copy constructor or copy factory:
* They don't rely on a risk-prone extralinguistic object creation mechanism.
* They don't demand unenforceable adherence to thinly documented conventions.
* They don't conflict with the proper use of final fields.
* They don't throw unnecessary checked exceptions.
* They don't require casts.
* They can take an argument whose type is an interface implemented by the class.
* Interface-based copy constructors and factories (_conversion_ constructors and _conversion_ factories) allow the client to accept the implementation type of the original.

### Consider implementing `Comparable`

The notation `sgn`(expression) designates the mathematical _signum_ function, which is defined to return -1, 0, or 1

* The implementor must ensure that `sgn(x.compareTo(y)) == -sgn(y. compareTo(x))` for all `x` and `y`. Implies that `x.compareTo(y)` must throw an exception if and only if `y.compareTo(x)` throws an exception.
* Transitive: ``(x. compareTo(y) > 0 && y.compareTo(z) > 0)`` implies `x.compareTo(z) > 0`.
* `x.compareTo(y) == 0` implies that `sgn(x.compareTo(z)) == sgn(y.compareTo(z))`, for all `z`.
* It is strongly recommended, but not required, that `(x.compareTo(y) == 0) == (x.equals(y))`.

Use of the relational operators `<` and `>` in compareTo methods is verbose and error-prone and no longer recommended.

If a class has multiple significant fields, the order in which you compare them is critical. Start with the most significant field and work your way down.

The `Comparator` interface is outfitted with a set of comparator construction methods, which enable fluent construction of comparators. Many programmers prefer the conciseness of this approach, though it does come at a modest performance cost.

```java
private static final Comparator<PhoneNumber> COMPARATOR =
    comparingInt((PhoneNumber pn) -> pn.areaCode)
        .thenComparingInt(pn -> pn.prefix)
        .thenComparingInt(pn -> pn.lineNum);

public int compareTo(PhoneNumber pn) {
    return COMPARATOR.compare(this, pn);
}
```

**Avoid comparators based on differences, they violate transitivity**

```java
static Comparator<Object> hashCodeOrder = new Comparator<>() {
    public int compare(Object o1, Object o2) {
        return o1.hashCode() - o2.hashCode();
    }
};
```

## Classes and interfaces

### Minimise the accessibility of classes and members

A well-designed component hides all its implementation details, cleanly separating their API from its implementation.

Information hiding or _encapsulation_ is important because:
* _Decouples_ the component that comprise the system, allowing them to be developed, tested, optimised, used, understood and modified in isolation.
* Speeds up development because components can be developed in parallel.
* Eases the burden of maintenance because components can be understood more quickly and debugged or replaced with little fear or harming other components.
* Components can be optimised without affecting correctness of others.
* Increases software reuse because components that aren't tightly coupled often prove useful in other contexts.
* Decreases the risk in building large systems because individual components may prove successful even if the system does not.

Make each class or member as inaccessible as possible.

Instance fields of public classes should rarely be public. Classes with public mutable fields are generally thread-safe.

Nonzero-length array is always mutable, so it is wrong for a class to have a public static final array field, or accessor that returns such a field. It is a potential security hole.

```java
public static final Thing[] VALUES = { ... };
```

Alternatively, return a copy of a private array

```java
private static final Thing[] PRIVATE_VALUES = { ... };

public static final List<Thing> VALUES =
   Collections.unmodifiableList(Arrays.asList(PRIVATE_VALUES));
```

### In public classes, use accessor methods, not public fields

Degenerate classes like this should not be public

```java
class Point {
   public double x;
   public double y;
}
```

Because the data fields of such classes are accessed directly, these classes do not offer the benefits of _encapsulation_. You can't change the representation without changing the API, you can't enforce invariants, and you can't take auxiliary action when a field is accessed.

If a class is accessed outside its package, provide accessor methods.

If a class is package-private or is a private nested class, there is nothing inherently wrong with exposing its data fields.

### Minimise mutability

An immutable class is simply a class whose instances cannot be modified. **Immutable classes are easier to design, implement, and use than mutable classes. They are less prone to error and are more secure.**

1. Don't provide methods that modify the object's state (mutators).
2. Ensure that the class can't be extended.
3. Make all fields final.
4. Make all fields private.
5. Ensure exclusive access to any mutable components.

Returning new objects on operations is known as _functional approach_ because methods return the result of applying a function to their operand, without modifying it. Contrast it to the _procedural_ or _imperative_ approach in which methods apply a procedure to their operand, causing its state to change. **Method names in immutable objects are prepositions (such as `plus`) rather than names (such as `add`).**

Advantages of immutable objects:
* Simple.
* Inherently thread-safe; they require no synchronisation.
* Can be shared freely.
* Not only you can share immutable objects, but they can share their internals.
* Make great building blocks for other objects.
* Provide failure atomicity for free. There is no possibility of temporary inconsistency.

The main disadvantage immutable objects have is that they require a separate object for each distinct value.

Classes should be immutable unless there's a very good reason to make them mutable.

If a class cannot be made immutable, limit its mutability as much as possible. Declare every field `private final` unless there's a good reason to do otherwise.

Constructors should create fully initialised objects with all of their invariants established.

### Favour composition over inheritance

Using inheritance inappropriately lead to fragile software. It is safe to use inheritance within a package where programmers have classes and subclasses under control. It is safe to use inheritance when extending classes specifically designed and documented for extension.

Unlike method invocation, implementation inheritance violates encapsulation. Subclasses depend on the implementation details of its superclass for its proper function.

To avoid fragility use composition and forwarding instead of inheritance, especially if an appropriate interface to implement a wrapper exists. Wrapper classes are not only more robust than subclasses, they are also more powerful.

### Design and document for inheritance or else prohibit it

The class must document its self-use of overridable methods.

A class may have to provide hooks into its internal workings in the form of judiciously chosen protected methods.

**The only way to test a class designed for inheritance is to write subclasses.**

You must test your class by writing subclasses before you release it.

Constructors must not invoke overridable methods. Superclass constructor runs before the subclass constructor. If the overriding method depends on any initialisation performed by the subclass constructor, the method will not behave as expected.

```java
public class Super {
    // Broken - constructor invokes an overridable method
    public Super() {
        overrideMe();
    }

    public void overrideMe() {
    }
}

public final class Sub extends Super {
    // Blank final, set by constructor
    private final Instant instant;

    Sub() {
        instant = Instant.now();
    }

    // Overriding method invoked by superclass constructor
    @Override public void overrideMe() {
        System.out.println(instant);
    }

    public static void main(String[] args) {
        Sub sub = new Sub();//null
        sub.overrideMe();//instant
    }
}
```

Same restriction applies to `clone` and `readObject`, they should not invoke overridable methods, directly or indirectly.

Designing a class for inheritance requires great effort and places substantial limitations on the class.

The best solution to this problem is to prohibit subclassing in classes that are not designed and documented to be safely subclassed. There are two ways of doing this. Declare the class final or make all constructors private or package-private and to add public static factories instead of constructors.

### Prefer interfaces to abstract classes

Existing classes can easily be retrofitted to implement a new interface.

Interfaces are ideal for defining _mixings_, a type that a class can implement in addition to its "primary type". For example Comparable is a mixing that allows a class can be ordered.

Interfaces allow for the construction of nonhierarchical type frameworks.

Interfaces enable safe, powerful functionality enhancements via the wrapper class idiom. If you use abstract classes, you leave the programmer who wants to add functionality with no alternative than to use inheritance.

You can combine the advantages of interfaces and abstract classes by providing an abstract _skeletal implementation class_ to go with an interface. The interface defines the type, while the skeletal implementation class implements the primitive interface methods (_Template Method_ pattern).

Concrete implementation built on top of an skeletal implementation.

```java
static List<Integer> intArrayAsList(int[] a) {
    Objects.requireNonNull(a);

    // The diamond operator is only legal here in Java 9 and later
    // If you're using an earlier release, specify <Integer>
    return new AbstractList<>() {
        @Override public Integer get(int i) {
            return a[i];  // Autoboxing (Item 6)
        }

        @Override public Integer set(int i, Integer val) {
            int oldVal = a[i];
            a[i] = val;     // Auto-unboxing
            return oldVal;  // Autoboxing
        }

        @Override public int size() {
            return a.length;
        }
    };
}
```
Skeletal implementation classes provide implementation assistance of abstract classes without imposing constraints as type definitions.

Good documentation is essential in a skeletal implementation.

### Design interfaces for posterity

It is not always possible to write a default method that maintains all the invariants of every conceivable implementation.

In the presence of default methods, existing implementations of an interface may compile without error or warning but fail at runtime.

Is still of the utmost importance to design interfaces with great care. While it may be possible to correct some interface flaws after an interface is released, you cannot count on it.

### Use interfaces only to define types

Constant interface anti-pattern (only constants) are a poor use of interfaces. Implementing a constant interface causes this implementation detail to leak into the class's exported API.

```java
public interface PhysicalConstants {
    static final double AVOGADROS_NUMBER   = 6.022_140_857e23;
    static final double BOLTZMANN_CONSTANT = 1.380_648_52e-23;
    static final double ELECTRON_MASS      = 9.109_383_56e-31;
}
```

If the constants are strongly tied to a class or interface, you should add them there. If not, a utility class are a good choice

```java
public class PhysicalConstants {
  private PhysicalConstants() { }  // Prevents instantiation

  public static final double AVOGADROS_NUMBER = 6.022_140_857e23;
  public static final double BOLTZMANN_CONST  = 1.380_648_52e-23;
  public static final double ELECTRON_MASS    = 9.109_383_56e-31;
}
```

### Prefer class hierarchies to tagged classes

Tagged class, vastly inferior to a class hierarchy.

```java
class Figure {
    enum Shape { RECTANGLE, CIRCLE };

    // Tag field - the shape of this figure
    final Shape shape;

    // These fields are used only if shape is RECTANGLE
    double length;
    double width;

    // This field is used only if shape is CIRCLE
    double radius;

    // Constructor for circle
    Figure(double radius) {
        shape = Shape.CIRCLE;
        this.radius = radius;
    }

    // Constructor for rectangle
    Figure(double length, double width) {
        shape = Shape.RECTANGLE;
        this.length = length;
        this.width = width;
    }

    double area() {
        switch(shape) {
          case RECTANGLE:
            return length * width;
          case CIRCLE:
            return Math.PI * (radius * radius);
          default:
            throw new AssertionError(shape);
        }
    }
}
```

Tagged classes are verbose, error-prone and inefficient.

A tagged class is just a pallid imitation of a class hierarchy.

With class hierarchy

```java
abstract class Figure {
    abstract double area();
}

class Circle extends Figure {
    final double radius;

    Circle(double radius) { this.radius = radius; }

    @Override double area() { return Math.PI * (radius * radius); }
}

class Rectangle extends Figure {
    final double length;
    final double width;

    Rectangle(double length, double width) {
        this.length = length;
        this.width  = width;
    }

    @Override double area() { return length * width; }
}
```

### Favour static member classes over nonstatic

Typical use of a nonstatic member class

```java
public class MySet<E> extends AbstractSet<E> {
    ... // Bulk of the class omitted

    @Override public Iterator<E> iterator() {
        return new MyIterator();
    }

    private class MyIterator implements Iterator<E> {
        ...
    }

}
```

If you declare a member class that does not require access to an enclosing instance, always put the `static` modifier in its declaration. If you omit this modifier, each instance will have a hidden extraneous reference to its enclosing instance and it will take time and space.

### Limit source files to a single top-level class

Use static member classes instead of multiple top-level classes. If you do otherwise, your program might not be able to compile or run properly.

```java
public class Test {
    public static void main(String[] args) {
        System.out.println(Utensil.NAME + Dessert.NAME);
    }

    private static class Utensil {
        static final String NAME = "pan";
    }

    private static class Dessert {
        static final String NAME = "cake";
    }
}
```

Never put multiple top-level classes or interfaces in a single source file.

## Generics

### Don't use raw types

```java
private final Collection stamps = ... ;
```

If you use raw types, you lose all the safety and expressiveness benefits of generics.

```java
private final Collection<Stamp> stamps = ... ;
```

You lose type safety if you use a raw type such as `List`, but not if you use a parameterised type such as `List<Object>`.

This method works but it uses raw types, which is dangerous.

```java
static int numElementsInCommon(Set s1, Set s2) {
    int result = 0;
    for (Object o1 : s1)
        if (s2.contains(o1))
            result++;
    return result;
}
```

Better to use wildcard type.

```java
static int numElementsInCommon(Set<?> s1, Set<?> s2) { ... }
```

You can put _any_ element into a collection with a raw type, easily corrupting the collection type invariant. **You can't put any element (other than null) into a `Collection<?>`**

There are a couple of exceptions to the use of raw types
* You must use raw types in class literals, as `List.class` is legal, but `List<String>.class` is not.
* Raw types is the preferred way to use the `instanceof` operator with generic types
    ```java
    if (o instanceof Set) {       // Raw type
        Set<?> s = (Set<?>) o;    // Wildcard type
        ...
    }
    ```

### Eliminate unchecked warnings

Eliminate every unchecked warning that you can. That will ensure your code is typesafe.

If you can't eliminate a warning, but you can prove that the code that provoked the warning is typesafe, then (and only then) suppress the warning with an `@SupressWarnings("unchecked")` annotation.

Always use the `SuppressWarnings` annotation on the smallest scope possible.

Every time you use a `@SuppressWarnings("unchecked")` annotation, add a comment saying why it is safe to do so.

### Prefer lists to arrays

Arrays are _covariant_, which means that if a `Sub` is a subtype of `Super`, then array type `Sub[]` is a subtype of the array type `Super[]`. Generics, by contrast, are _invariant_, for any two distinct types `Type1` and `Type2`, `List<Type1>` is neither a subtype or a supertype of `List<Type2>`.

Arrays are deficient, this code fragment is legal and it fails at runtime

```java
Object[] objectArray = new Long[1];
objectArray[0] = "I don't fit in"; // Throws ArrayStoreException
```

This one won't compile

```java
List<Object> ol = new ArrayList<Long>(); // Incompatible types
ol.add("I don't fit in");
```

### Favour generic types

Generic types are safer and easier to use than types that require casts in client code.When you design new types, make sure that they can be used without such casts.

### Favour generic methods

Generic methods, like generic types, are safer and easier to use than methods requiring their clients to put explicit casts on input parameters and return types.

### Use bounded wildcards to increase API flexibility

Wildcard type for a parameter that serves as an E producer

```java
public void pushAll(Iterable<? extends E> src) {
    for (E e : src)
        push(e);
}
```

This would make `Stack<Number>` work also on `stack.pushAll(intVal)`, as `Integer` is a subtype of `Number`.

Sometimes we would want to do the opposite, have a wildcard type for parameter that serves as an `E` consumer.

```java
public void popAll(Collection<? super E> dst) {
    while (!isEmpty())
        dst.add(pop());
}
```

So we can do

```java
Collection<Object> objects = ...;
numberStack.popAll(objects);
```

For maximum flexibility, use wildcard types on input parameters that represent producers or consumers.

_PECS_ stands for producer-`extends` and consumer-`super`.

Do not use bounded wildcard types as return types. It would force wildcard types on client code.

**If the user of a class has to think about wildcard types, there is probably something wrong with its API.**

If a type parameter appears only once in a method declaration, replace it  with a wildcard.

### Combine generics and varargs judiciously

Mixing generics and varargs can violate type safety.

```java
static void dangerous(List<String>... stringLists) {
    List<Integer> intList = List.of(42);
    Object[] objects = stringLists;
    objects[0] = intList;             // Heap pollution
    String s = stringLists[0].get(0); // ClassCastException
}
```

It is unsafe to store a value in a generic varargs array parameter.

The `SafeVarargs` annotation constitutes a promise by the author of a method that it is typesafe.

This is unsafe, it exposes a reference to its generic parameter array. The compiler might not have enough information to make an accurate determination of the type of the argument and it can propagate heap pollution up the stack.

```java
static <T> T[] toArray(T... args) {
    return args;
}
```

It is unsafe to give another method access to a generic varargs parameter array.

Safe method with a generic varargs parameter
```java
@SafeVarargs
static <T> List<T> flatten(List<? extends T>... lists) {
    List<T> result = new ArrayList<>();
    for (List<? extends T> list : lists)
        result.addAll(list);
    return result;
}
```

Use `@SafeVarargs` on every method with a varargs parameter of a generic or parameterised type.

A generic varargs method is safe if:
1. Does not store anything in the varargs parameter array
2. Does not make the array (or a clone) visible to untrusted code.

Use `List` as a typesafe alternative to a generic varargs parameter

```java
static <T> List<T> flatten(List<List<? extends T>> lists) {
    List<T> result = new ArrayList<>();
    for (List<? extends T> list : lists)
        result.addAll(list);
    return result;
}
```

### Consider typesafe heterogeneous containers

Typesafe heterogeneous container pattern API

```java
public class Favorites {
    public <T> void putFavorite(Class<T> type, T instance);
    public <T> T getFavorite(Class<T> type);
}
```

Typesafe heterogeneous container pattern client

```java
public static void main(String[] args) {

    Favorites f = new Favorites();

    f.putFavorite(String.class, "Java");

    f.putFavorite(Integer.class, 0xcafebabe);

    f.putFavorite(Class.class, Favorites.class);


    String favoriteString = f.getFavorite(String.class);

    int favoriteInteger = f.getFavorite(Integer.class);

    Class<?> favoriteClass = f.getFavorite(Class.class);

    System.out.printf("%s %x %s%n", favoriteString,

        favoriteInteger, favoriteClass.getName());

}
```

A `Favorites` instance is _typesafe_: it will never return an `Integer` when you ask it for a `String`. It is also _heterogeneous_: unlike an ordinary map, all the keys are of different types. Therefore, we call `Favorites` a _typesafe heterogeneous container_.

Typesafe heterogeneous container pattern - implementation

```java
public class Favorites {
    private Map<Class<?>, Object> favorites = new HashMap<>();

    public <T> void putFavorite(Class<T> type, T instance) {
        favorites.put(Objects.requireNonNull(type), instance);
    }

    public <T> T getFavorite(Class<T> type) {
        return type.cast(favorites.get(type));
    }
}
```

Achieving runtime type safety with a dynamic cast

```java
public <T> void putFavorite(Class<T> type, T instance) {
    favorites.put(type, type.cast(instance));
}
```

## Enums and annotations

### Use enums instead of int constants

The _`int` enum pattern_ provides nothing in the way of type safety and little in the way of expressive power.

```java
public static final int APPLE_FUJI         = 0;
public static final int APPLE_PIPPIN       = 1;
public static final int APPLE_GRANNY_SMITH = 2;
public static final int ORANGE_NAVEL  = 0;
public static final int ORANGE_TEMPLE = 1;
public static final int ORANGE_BLOOD  = 2;
```

```java
public enum Apple  { FUJI, PIPPIN, GRANNY_SMITH }
public enum Orange { NAVEL, TEMPLE, BLOOD }
```

Java's enum types are classes that export one instance for each enumeration constant via a public static field num. Enum are effectively final because they have no accessible constructors.

They are type safe, if you declare a parameter to be of type `Apple`, you are guaranteed that any non-null object reference passed to the parameter is one of the three valid `Apple` values.

Enum types let you add arbitrary methods, provide high-quality implementations of all the `Object` methods, they implement `Comparable` and `Serializable`.

To associate data with enum constants, declare instance fields and write constructor that takes the data and stores it in the fields.

Enum type that switches on its own value, questionable.

```java
public enum Operation {
    PLUS, MINUS, TIMES, DIVIDE;

    // Do the arithmetic operation represented by this constant
    public double apply(double x, double y) {
        switch(this) {
            case PLUS:   return x + y;
            case MINUS:  return x - y;
            case TIMES:  return x * y;
            case DIVIDE: return x / y;
        }
        throw new AssertionError("Unknown op: " + this);
    }
}
```

Enum type with constant-specific method implementations

```java
public enum Operation {
  PLUS  {public double apply(double x, double y){return x + y;}},
  MINUS {public double apply(double x, double y){return x - y;}},
  TIMES {public double apply(double x, double y){return x * y;}},
  DIVIDE{public double apply(double x, double y){return x / y;}};

  public abstract double apply(double x, double y);
}
```

Enum type with constant-specific class bodies and data

```java
public enum Operation {
    PLUS("+") {
        public double apply(double x, double y) { return x + y; }
    },
    MINUS("-") {
        public double apply(double x, double y) { return x - y; }
    },
    TIMES("*") {
        public double apply(double x, double y) { return x * y; }
    },
    DIVIDE("/") {
        public double apply(double x, double y) { return x / y; }
    };

    private final String symbol;

    Operation(String symbol) { this.symbol = symbol; }

    @Override public String toString() { return symbol; }

    public abstract double apply(double x, double y);
}
```

**Use enums any time you need a set of constants whose members are known at compile time.** It is not necessary that the set of constants in an enum type stay fixed for all time, the enum was specifically designed to allow evolution of enum types.

### Use instance fields instead of ordinals

Abuse of ordinal to derive an associated value, **don't do this**.

```java
public enum Ensemble {
    SOLO,   DUET,   TRIO, QUARTET, QUINTET,
    SEXTET, SEPTET, OCTET, NONET,  DECTET;

    public int numberOfMusicians() { return ordinal() + 1; }
}
```

Never derive a value associated with an enum from its ordinal; store it in an instance field instead.

```java
public enum Ensemble {
    SOLO(1), DUET(2), TRIO(3), QUARTET(4), QUINTET(5),
    SEXTET(6), SEPTET(7), OCTET(8), DOUBLE_QUARTET(8),
    NONET(9), DECTET(10), TRIPLE_QUARTET(12);

    private final int numberOfMusicians;

    Ensemble(int size) { this.numberOfMusicians = size; }
    public int numberOfMusicians() { return numberOfMusicians; }
}
```

### Use `EnumSet` instead of bit fields

Bit field enumeration constants, obsolete.

```java
public class Text {
    public static final int STYLE_BOLD          = 1 << 0;  // 1
    public static final int STYLE_ITALIC        = 1 << 1;  // 2
    public static final int STYLE_UNDERLINE     = 1 << 2;  // 4
    public static final int STYLE_STRIKETHROUGH = 1 << 3;  // 8

    // Parameter is bitwise OR of zero or more STYLE_ constants
    public void applyStyles(int styles) { ... }
}
```

This representation lets you use the bitwise `OR` operation to combine several constants into a set, known as a _bit field_

```java
text.applyStyles(STYLE_BOLD | STYLE_ITALIC);
```

_Bit fields_ have all the disadvantages than `int` enum pattern. A better alternative is to use `EnumSet`

```java
public class Text {
    public enum Style { BOLD, ITALIC, UNDERLINE, STRIKETHROUGH }

    // Any Set could be passed in, but EnumSet is clearly best
    public void applyStyles(Set<Style> styles) { ... }
}
```

So you could use it like

```java
text.applyStyles(EnumSet.of(Style.BOLD, Style.ITALIC));
```

**Just because an enumerated type will be used in sets, there is no reason to represent it with bit fields.**

### Use `EnumMap` instead of ordinal indexing

```java
class Plant {
    enum LifeCycle { ANNUAL, PERENNIAL, BIENNIAL }

    final String name;
    final LifeCycle lifeCycle;

    Plant(String name, LifeCycle lifeCycle) {
        this.name = name;
        this.lifeCycle = lifeCycle;
    }

    @Override public String toString() {
        return name;
    }
}
```

Using `ordinal()` to index into an array, **don't do this**.

```java
Set<Plant>[] plantsByLifeCycle =
    (Set<Plant>[]) new Set[Plant.LifeCycle.values().length];

for (int i = 0; i < plantsByLifeCycle.length; i++)
    plantsByLifeCycle[i] = new HashSet<>();

for (Plant p : garden)
    plantsByLifeCycle[p.lifeCycle.ordinal()].add(p);

// Print the results
for (int i = 0; i < plantsByLifeCycle.length; i++) {
    System.out.printf("%s: %s%n",
        Plant.LifeCycle.values()[i], plantsByLifeCycle[i]);
}
```

Using an `EnumMap` to associate data with an enum

```
Map<Plant.LifeCycle, Set<Plant>>  plantsByLifeCycle =
    new EnumMap<>(Plant.LifeCycle.class);
for (Plant.LifeCycle lc : Plant.LifeCycle.values())
    plantsByLifeCycle.put(lc, new HashSet<>());
for (Plant p : garden)
    plantsByLifeCycle.get(p.lifeCycle).add(p);
System.out.println(plantsByLifeCycle);
```

Or even a shorter version, a bit naive as it doesn't produce an `EnumMap`

```java
System.out.println(Arrays.stream(garden)
    .collect(groupingBy(p -> p.lifeCycle)));
```

Fixed version

```java
System.out.println(Arrays.stream(garden)
    .collect(groupingBy(p -> p.lifeCycle,
        () -> new EnumMap<>(LifeCycle.class), toSet())));
```

**It is rarely appropriate to use ordinals to index into arrays: use EnumMap instead**.

### Emulate extensible enums with interfaces

In the case for _opcodes_, _operation codes_ that represent operations in some machine, is desirable to let the user of an API provide their own operations, effectively extending the set of operations provided by the API.

You can do this by implementing interfaces.

```java
public interface Operation {
    double apply(double x, double y);
}

public enum BasicOperation implements Operation {
    PLUS("+") {
        public double apply(double x, double y) { return x + y; }
    },
    MINUS("-") {
        public double apply(double x, double y) { return x - y; }
    },
    TIMES("*") {
        public double apply(double x, double y) { return x * y; }
    },
    DIVIDE("/") {
        public double apply(double x, double y) { return x / y; }
    };
    private final String symbol;

    BasicOperation(String symbol) {
        this.symbol = symbol;
    }

    @Override public String toString() {
        return symbol;
    }
}
```

And an emulated extension enum

```java
public enum ExtendedOperation implements Operation {
    EXP("^") {
        public double apply(double x, double y) {
            return Math.pow(x, y);
        }
    },
    REMAINDER("%") {
        public double apply(double x, double y) {
            return x % y;
        }
    };

    private final String symbol;

    ExtendedOperation(String symbol) {
        this.symbol = symbol;
    }

    @Override public String toString() {
        return symbol;
    }
}
```

Now you can use your new operations anywhere you could use the basic operations, provided that API's are written to take the interface type `Operation`, not the implementation `BasicOperation`.

```java
private void test(Collection<? extends Operation> opSet);
```

While you cannot write an extensible enum type, you can emulate it by writing an interface to accompany a basic enum type that implements the interface.

### Prefer annotations to naming patterns

It's been common to use _naming patterns_ to indicate that some program elements demanded special treatment by a tool or framework. Like prefixing your tests with `test` word, so JUnit 3 would pick it up. These have many disadvantages:
1. Typographical errors result in silent failures. Imagine you accidentally named a test method `tsetSomething` instead of `testSomething`. JUnit 3 wouldn't complain, but it wouldn't run the test either.
2. There is no way to ensure that they are used only on appropriate program elements. Imagine creating a class `TestSafetyMechanism` in the hopes that JUnit 3 would automatically test its methods.
3. They provide no good way to associate parameter values with program elements. Suppose you want to support a category of test that succeeds only if it throws a particular exception, the exception type is the parameter of the test. You could encode the exception type in the test name but the compiler would have no way of knowing to check the string that was supposed to name the exception.

Annotations solve all these problems nicely, and JUnit adopted them starting with release 4.

Marker annotation type declaration

```java
import java.lang.annotation.*;

/**
 * Indicates that the annotated method is a test method.
 * Use only on parameterless static methods.
 */
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface Test {
}
```

Program to process marker annotations

```java
import java.lang.reflect.*;

public class RunTests {
    public static void main(String[] args) throws Exception {
        int tests = 0;
        int passed = 0;
        Class<?> testClass = Class.forName(args[0]);
        for (Method m : testClass.getDeclaredMethods()) {
            if (m.isAnnotationPresent(Test.class)) {
                tests++;
                try {
                    m.invoke(null);
                    passed++;
                } catch (InvocationTargetException wrappedExc) {
                    Throwable exc = wrappedExc.getCause();
                    System.out.println(m + " failed: " + exc);
                } catch (Exception exc) {
                    System.out.println("Invalid @Test: " + m);
                }
            }
        }
        System.out.printf("Passed: %d, Failed: %d%n",
                          passed, tests - passed);
    }
}
```

There is no reason to use naming patterns when you can use annotations instead.

With the exception of toolshmiths, most programmers will have no need to define annotation types. All programmers should use the predefined annotations types that Java provides.

### Consistently use the override annotation

Buggy code, spot the error.

```java
public boolean equals(Bigram b) {
    return b.first == first && b.second == second;
}
```

With an `Override`, the program won't compile

```java
@Override public boolean equals(Bigram b) {
    return b.first == first && b.second == second;
}
```

Override will check overriding method at compile time. `equals` requires the parameter to be type `Object`. The fixed version

```java
@Override public boolean equals(Object o) {
    if (!(o instanceof Bigram))
        return false;

    Bigram b = (Bigram) o;
    return b.first == first && b.second == second;

}
```

Use the `Override` annotation on every method declaration that you believe to override a superclass declaration.

### Use marker interfaces to define types

A _marker interface_ is an interface that contains no method declarations but merely designates (or "marks") a class that implements the interface as having some property. An example of this is the `Serializable` interface.

Marker interfaces define a type that is implemented by instances of the marked class; marker annotations do not. **The existence of a marker interface type allows you to catch errors at compile time that you couldn't catch until runtime if you used a marker annotation.**

Another advantage of marker interfaces over marker annotations is that they can be targeted more precisely. If an annotation is declared with target `ElementType.TYPE`, it can be applied to _any_ class or interface.

The chief advantage of a marker annotation over marker interfaces is that they are part of the larger annotation facility. Marker annotations allow for consistency in annotation-based frameworks.

If you find yourself writing a marker annotation type whose target is `ElementType.TYPE`, take the time to figure out whether it is really should be an annotation type or whether a marker interface would be more appropriate.

## Lambdas and streams

### Prefer lambdas to anonymous classes

Obsolete

```java
Collections.sort(words, new Comparator<String>() {
    public int compare(String s1, String s2) {
        return Integer.compare(s1.length(), s2.length());
    }
});
```

Lambda expression as function object

```java
Collections.sort(words,
        (s1, s2) -> Integer.compare(s1.length(), s2.length()));
```

Omit the types of all lambda parameters unless their presence makes your program clearer.

Enum with function object fields and constant-specific behaviour

```java
public enum Operation {
    PLUS  ("+", (x, y) -> x + y),
    MINUS ("-", (x, y) -> x - y),
    TIMES ("*", (x, y) -> x * y),
    DIVIDE("/", (x, y) -> x / y);

    private final String symbol;
    private final DoubleBinaryOperator op;

    Operation(String symbol, DoubleBinaryOperator op) {
        this.symbol = symbol;
        this.op = op;
    }

    @Override public String toString() { return symbol; }

    public double apply(double x, double y) {
        return op.applyAsDouble(x, y);
    }
}
```

Lambdas lack names and documentation; if a computation isn't self-explanatory, or exceeds a few lines (more than three), don't put it in a lambda.


You should rarely, if eve, serialise a lambda.

Don't use anonymous classes for function objects unless you have to create instances of types that aren't functional interfaces.

### Prefer method references to lambdas

Where method references are shorter and clearer, use them; where they aren't, stick with lambdas.

```java
map.merge(key, 1, (count, incr) -> count + incr);
```

to

```java
map.merge(key, 1, Integer::sum);
```

All kinds of method references are summarised below

Method Ref Type   | Example                  | Lambda equivalent
------------------|--------------------------|------------------------------------------------------
Static            | `Integer::parseInt`      | `str -> Integer.parseInt(str)`
Bound             | `Instant.now()::isAfter` | `Instant then = Instant.now(); t -> then.isAfter(t)`
Unbound           | `String::toLowerCase`    | `str -> str.toLowerCase()`
Class Constructor | `TreeMap<K,V>::new`      | `() -> new TreeMap<K,V>`
Array Constructor | `int[]::new`             | `len -> new int[len]`

### Favour the use of standard functional interfaces

Unnecessary functional interface; use a standard one instead.

```java
@FunctionalInterface interface EldestEntryRemovalFunction<K,V>{
    boolean remove(Map<K,V> map, Map.Entry<K,V> eldest);
}
```

If one of the standard functional interfaces does the job, you should generally use it in preference to a purpose-built functional interface.

The six basic functional interfaces are summarised below

Interface           | Function Signature    | Example
--------------------|-----------------------|-----------------------
`UnaryOperator<T>`  | `T apply(T t)`        | `String::toLowerCase`
`BinaryOperator<T>` | `T apply(T t1, T t2)` | `BigInteger::add`
`Predicate<T>`      | `boolean test(T t)`   | `Collection::isEmpty`
`Function<T,R>`     | `R apply(T t)`        | `Arrays::asList`
`Supplier<T>`       | `T get()`             | `Instant::now`
`Consumer<T>`       | `void accept(T t)`    | `System.out.println`

Don't be tempted to use basic functional interfaces with boxed primitives instead of primitive functional interfaces (prefer primitive types to boxed primitives, performance will suffer otherwise).

**Always annotate your functional interfaces with the `@FunctionalInterface` annotation.** Its behaviour is similar to `@Override`, it tells the readers that the class was designed to enable lambdas; it won't compile unless it has exactly one abstract method; it prevents maintainers from accidentally adding abstract methods to the interface as it evolves.

### Use streams judiciously

```java
words.collect(groupingBy(word -> alphabetize(word)))
      .values().stream()
      .filter(group -> group.size() >= minGroupSize)
      .forEach(g -> System.out.println(g.size() + ": " + g));
```

Stream pipelines are evaluated `lazily`, evaluation doesn't start until the terminal operation is invoked.

Overusing streams makes programs hard to read and maintain.

In the absence of explicit types, careful naming of lambda parameters is essential to the readability of stream pipelines.

Using helper methods is even more important for readability in stream pipelines than in iterative code because pipelines lack explicit type information.

If you are not sure whether a task is better served by streams or iteration, try both and see which works better.

### Prefer side-effect-free functions in streams

The following code uses the streams API but not the paradigm, don't do this.

```
Map<String, Long> freq = new HashMap<>();
try (Stream<String> words = new Scanner(file).tokens()) {
    words.forEach(word -> {
        freq.merge(word.toLowerCase(), 1L, Long::sum);
    });
}
```

Proper use of streams

```
Map<String, Long> freq;
try (Stream<String> words = new Scanner(file).tokens()) {
    freq = words
        .collect(groupingBy(String::toLowerCase, counting()));
}
```

**The `forEach` operation should be used only to report the result of a stream computation, not to perform the computation.**

Pipeline to get a top-ten list of words from a frequency table

```java
List<String> topTen = freq.keySet().stream()
    .sorted(comparing(freq::get).reversed())
    .limit(10)
    .collect(toList());
```

**It is customary and wise to statically import all members of `Collectors` because it makes stream pipelines more readable.**

### Prefer `Collection` to `Stream` as a return type

Streams do not make iteration obsolete, writing good code requires combining streams and iteration judiciously.

The `Collection` interface is a subtype of `Iterable` and has a `stream` method, so it provides both iteration and stream access. **`Collection` or an appropriate subtype is generally the best return type for a public, sequence-returning method.** But do not store large sequence in memory just to return it as a collection. If the sequence you're returning is large but can be represented concisely, consider implementing a special-purpose collection.

### Use caution when making streams parallel

Parallelising a pipeline is unlikely to increase its performance if the source is from `Stream.iterate`, or the intermediate operation `limit` is used.

Do not parallelise stream pipelines indiscriminately.

As a rule, performance gains from parallelism are best on streams over `ArrayList`, `HashMap`, `HashSet`, and `ConcurrentHashMap` instances; arrays; `int` ranges; and `long` ranges. What all these data structures have in common is that they can be cheaply split into subranges of any desired sizes, which makes them easy to divide work among parallel threads.

**Not only can parallelising a stream lead to poor performance, including liveness failures; it can lead to incorrect results and unpredictable behaviour.**

Under the right circumstances, it is possible to achieve near-linear speedup in the number of processor cores simply by adding a `parallel` call to a stream pipeline.

## Methods

### Check parameters for validity

Each time you write a method or constructor, you should think about what restrictions exist on its parameters. You should document these restrictions and enforce them with explicit checks at the beginning of the method body.

If an invalid parameter value is passed to a method and the method checks its parameters before execution, it will fail quickly and cleanly with an appropriate exception.

The `Objets.requireNonNull` method, added in Java 7, is flexible and convenient, so there's no reason to perform null checks manually anymore.

For an unexported method, you control the circumstances under which the method is called, so you can and should ensure that only valid parameter values are passed in. Nonpublic methods can check their parameters using _assertions_.

### Make defensive copies when needed

You must program defensively, with the assumption that clients of your class will do their best to destroy its invariants.

Broken "immutable" time period class

```java
public final class Period {
    private final Date start;
    private final Date end;

    /**
     * @param  start the beginning of the period
     * @param  end the end of the period; must not precede start
     * @throws IllegalArgumentException if start is after end
     * @throws NullPointerException if start or end is null
     */
    public Period(Date start, Date end) {
        if (start.compareTo(end) > 0)
            throw new IllegalArgumentException(
                start + " after " + end);
        this.start = start;
        this.end   = end;
    }

    public Date start() {
        return start;
    }

    public Date end() {
        return end;
    }
}
```

Attack the internals of `Period` instance

```java
Date start = new Date();
Date end = new Date();
Period p = new Period(start, end);
end.setYear(78);  // Modifies internals of p!
```

It is essential to make a defensive copy of each mutable parameter to the constructor.


Repaired constructor, makes defensive copies of parameters.

```java
public Period(Date start, Date end) {
    this.start = new Date(start.getTime());
    this.end   = new Date(end.getTime());

    if (this.start.compareTo(this.end) > 0)
      throw new IllegalArgumentException(
          this.start + " after " + this.end);
}
```

Defensive copies are made before checking the validity of the parameters, and the validity check is performed on the copies rather than the originals.

Do not use the `clone` method to make a defensive copy of a parameter whose type is subclassable by untrusted parties.

Second attack on the internals of a `Period` instance

```java
Date start = new Date();
Date end = new Date();
Period p = new Period(start, end);
p.end().setYear(78);  // Modifies internals of p!
```

Return defensive copies of mutable internal fields.

Repaired accessors, make defensive copies of internal fields

```java
public Date start() {
    return new Date(start.getTime());
}

public Date end() {
    return new Date(end.getTime());
}
```

You should, where possible, use immutable objects as components of your objects so that you don't have to worry about defensive copying.

### Design method signature carefully

* Choose method names carefully.
* Don't go overboard in providing convenience methods. When in doubt, leave it out.
* Avoid long parameter lists. Aim for four parameters or fewer. Long sequences of identically typed parameters are especially harmful.
*  For parameter types, favour interfaces over classes.
* Prefer two-element enum types to `boolean` parameters.
    ```java
    public enum TemperatureScale { FAHRENHEIT, CELSIUS }
    ```

### Use overloading judiciously

What does this program print?

```java
public class CollectionClassifier {
    public static String classify(Set<?> s) {
        return "Set";
    }

    public static String classify(List<?> lst) {
        return "List";
    }

    public static String classify(Collection<?> c) {
        return "Unknown Collection";
    }

    public static void main(String[] args) {
        Collection<?>[] collections = {
            new HashSet<String>(),
            new ArrayList<BigInteger>(),
            new HashMap<String, String>().values()
        };

        for (Collection<?> c : collections)
            System.out.println(classify(c));
    }
}
```

This program prints `Unknown Collection` three times, because **the choice of which overloading to invoke is made at compile time**.

The selection among overloaded methods is static, while selection among overriden methods is dynamic.

```java
class Wine {
    String name() { return "wine"; }
}

class SparklingWine extends Wine {
    @Override String name() { return "sparkling wine"; }
}

class Champagne extends SparklingWine {
    @Override String name() { return "champagne"; }
}

public class Overriding {
    public static void main(String[] args) {
        List<Wine> wineList = List.of(
            new Wine(), new SparklingWine(), new Champagne());

        for (Wine wine : wineList)
            System.out.println(wine.name());
    }
}
```

Avoid confusing choices of overloading.

A safe, conservative policy is never to export two overloading with the same number of parameters. You can always give methods different names instead of overloading them.

Do not overload methods to take different functional interfaces in the same argument position.

### Use _varargs_ judiciously

Simple use of varargs

```java
static int sum(int... args) {
    int sum = 0;
    for (int arg : args)
        sum += arg;
    return sum;
}
```

The **wrong** way to use varargs to pass one or more arguments. This program will fail at runtime instead of failing at compile time.

```java
static int min(int... args) {
    if (args.length == 0)
        throw new IllegalArgumentException("Too few arguments");
    int min = args[0];
    for (int i = 1; i < args.length; i++)
        if (args[i] < min)
            min = args[i];
    return min;
}
```

The right way to use varargs to pass one or more arguments

```java
static int min(int firstArg, int... remainingArgs) {
    int min = firstArg;
    for (int arg : remainingArgs)
        if (arg < min)
            min = arg;
    return min;
}
```

Exercise care when using varargs in performance-critical situations. Every invocation of a varargs method causes an array allocation and initialisation.

For these situations you can determine that 95% of the calls to a method have three or fewer parameters

```java
public void foo() { }
public void foo(int a1) { }
public void foo(int a1, int a2) { }
public void foo(int a1, int a2, int a3) { }
public void foo(int a1, int a2, int a3, int... rest) { }
```

### Return empty collections or arrays, not nulls

Returns null to indicate an empty collection. **Don't do this**.

```java
private final List<Cheese> cheesesInStock = ...;

/**
 * @return a list containing all of the cheeses in the shop,
 *     or null if no cheeses are available for purchase.
 */
public List<Cheese> getCheeses() {
    return cheesesInStock.isEmpty() ? null
        : new ArrayList<>(cheesesInStock);
}
```

There is no reason to special-case the situation where the no cheeses are available for purchase. Doing so requires extra code in the client to handle the possibly null return value

```java
List<Cheese> cheeses = shop.getCheeses();
if (cheeses != null && cheeses.contains(Cheese.STILTON))
    System.out.println("Jolly good, just the thing.");
```

The right way to return a possibly empty collection

```java
public List<Cheese> getCheeses() {
    return new ArrayList<>(cheesesInStock);
}
```

Optimisation, avoid allocating empty collections

```java
public List<Cheese> getCheeses() {
    return cheesesInStock.isEmpty() ? Collections.emptyList()
        : new ArrayList<>(cheesesInStock);
}
```

The right way to return a possibly empty array

```java
public Cheese[] getCheeses() {
    return cheesesInStock.toArray(new Cheese[0]);
}
```

Optimisation, avoids allocating empty arrays

```java
private static final Cheese[] EMPTY_CHEESE_ARRAY = new Cheese[0];

public Cheese[] getCheeses() {
    return cheesesInStock.toArray(EMPTY_CHEESE_ARRAY);
}
```

**Never return `null` in place for an empty array or collection.**

### Return optionals judiciously

Optionals are similar in spirit to checked exceptions. You should declare a method to return `Optional<T>` if it might not be able to return a result and clients will have to perform special processing if no result is returned.

Container types, including collections, maps, streams, arrays and optionals should not be wrapped in optionals. Rather than returning an empty `Optional<List<T>>`, you should simply return an empty `List<T>`.

Returning an optional that contains a boxed primitive is prohibitively expensive as it has two levels of boxing instead of zero. Library designers saw fit to provide analogues of Optional<T> for primitive types `int`, `long` and `double` (`OptionalInt`, `OptionalLong` and `OptionalDouble`). **You should never return an optional of a boxed primitive type.**

It is almost never appropriate to use an optional as a key, value, or element in a collection array.

Often storing an optional in an instance field is a "bad smell", but sometimes may be justified.

### Write doc comments for all exposed API elements

To document your API properly, you must precede every exported class, interface, constructor, method, and field declaration with a doc comments.

The doc comment for a method should describe succinctly the contract between the method and its client.

Doc comments should be readable both in the source code and in the generated documentation.

No two members or constructors in a class or interface should have the same summary description.

When documenting a generic type or method, be sure to document all type parameters.

```java
/**
 * An object that maps keys to values.  A map cannot contain
 * duplicate keys; each key can map to at most one value.
 *
 * (Remainder omitted)
 *
 * @param <K> the type of keys maintained by this map
 * @param <V> the type of mapped values
 */
public interface Map<K, V> { ... }
```

When documenting an enum type, be sure to document the constants.

```java
/**
 * An instrument section of a symphony orchestra.
 */
public enum OrchestraSection {
    /** Woodwinds, such as flute, clarinet, and oboe. */
    WOODWIND,

    /** Brass instruments, such as french horn and trumpet. */
    BRASS,

    /** Percussion instruments, such as timpani and cymbals. */
    PERCUSSION,

    /** Stringed instruments, such as violin and cello. */
    STRING;
}
```

When documenting an annotation type, be sure to document any members as the type itself.

```java
/**
 * Indicates that the annotated method is a test method that
 * must throw the designated exception to pass.
 */
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface ExceptionTest {
     /**
      * The exception that the annotated test method must throw
      * in order to pass. (The test is permitted to throw any
      * subtype of the type described by this class object.)
      */
    Class<? extends Throwable> value();
}
```

Whether or not a class or static method is thread-safe, you should document its thread-safely level.

The generated documentation should provide a clear description of your API. The only way to know for sure is to read the web pages generated by the Javadoc utility.

## General programming

### Minimise the scope of local variables

By minimising the scope of local variables, you increase the readability and maintainability of your code and reduce the likelihood for error.

**The most powerful technique for minimising the scope of a local variable is to declare it where it is first used.**

Nearly every local variable declaration should contain an initialiser.

Prefer `for` loops to `while` loops, as `for` loops limit the scope of the variables defined in their bodies.

Idiom for iterating when you need the iterator

```java
for (Iterator<Element> i = c.iterator(); i.hasNext(); ) {
    Element e = i.next();
    ... // Do something with e and i
}
```

A final technique to minimise the scope of local variables is to keep methods small and focused.

### Prefer `for-each` loops to traditional `for` loops

Not the best way to iterate over a collection

```java
for (Iterator<Element> i = c.iterator(); i.hasNext(); ) {
    Element e = i.next();
    ... // Do something with e
}
```

Not the best way to iterate over an array

```java
for (int i = 0; i < a.length; i++) {
    ... // Do something with a[i]
}
```

The iterator and the index variables are just clutter, all you need are the elements. They also represent opportunities for error. Also the two loops are quite different.

The preferred idiom for iterating over collections and arrays

```java
for (Element e : elements) {
    ... // Do something with e
}
```

Unfortunately, there are three common situations where you _can't_ use for-each:
* Destructive filtering
* Transforming
* Parallel iteration

In these cases you'll have to use an ordinary `for` loop and be wary of the problems they can generate.

### Know and use the libraries

Don't reinvent the wheel. If you need to do something that seems like it should be reasonably common, there may be already a facility in the libraries that does what you want.

By using a standard library, you take advantage of the knowledge of the experts who wrote it and the experience of those who used it before you.

The random number generator of choice is `ThreadLocalRandom`, it produces higher quality random numbers, and it's very fast.

Numerous features are added to the libraries in every major release, and it pays to keep abreast of these additions.

Every programer should be familiar with the basic of `java.lang`, `java.util` and `java.io` and their subpackages.

### Avoid `float` and `double` if exact answers are required

The `float` and `double` types are particularly ill-suited for monetary calculations because it is impossible to represent 0.1 as a `float` or `double` exactly.

Use `BigDecimal`, `int` or `long` for monetary calculations.

### Prefer primitive types to boxed primitives

Applying the `==` operator to boxed primitives is almost always wrong.

When you mix primitives and boxed primitives in an operation, the boxed primitive is auto-unboxed.

Autoboxing reduces the verbosity, but not the danger, of using boxed primitives. When your program does unboxing, it can throw a `NullPointerException`.

### Avoid strings where other types are more appropriate

* Strings are poor substitutes for other value types.
* Strings are poor substitutes for enum types.
* Strings are poor for aggregate types. `String compoundKey = className + "#" + i.next()`. If the character used to separate fields occurs in one the fields, chaos may result. To access individual fields you'll need to provide parsers. You can't provide `equals`, `toString` or `compareTo`. A better approach is to write a class.
* String are poor substitutes for capabilities. If a string represent a shared global namespace for a resource, two clients may independently and unintentionally use the same string causing both of them to fail. A better approach is to define an unforgeable key (or capability) to access to resources.

### Beware the performance of string concatenation

Using the string concatenation repeatedly to concatenate _n_ strings requires time quadratic in _n_.

Performs poorly

```java
public String statement() {
    String result = "";
    for (int i = 0; i < numItems(); i++)
        result += lineForItem(i);  // String concatenation
    return result;
}
```

To achieve acceptable performance, use `StringBuilder` in place of a `String`

```java
public String statement() {
    StringBuilder b = new StringBuilder(numItems() * LINE_WIDTH);
    for (int i = 0; i < numItems(); i++)
        b.append(lineForItem(i));
    return b.toString();
}
```

**Don't use the string concatenation operator to combine more than a few strings.**

### Refer to objects by their interfaces

If appropriate interface exists, then parameters, return values, variables, and field should all be declared using interface types.

Good, it uses interface as type

```java
Set<Son> sonSet = new LinkedHashSet<>();
```

Bad, it uses class as type

```java
LinkedHashSet<Son> sonSet = new LinkedHashSet<>();
```

**If you get into the habit of using interfaces as types, your program will be much more flexible.** If you decide to switch implementations, all you have to do is change the class name in the constructor.

It is entirely appropriate to refer to an object by a class rather than an interface if no appropriate interface exists.

When there is no appropriate interface, just use the least specific class int he class hierarchy that provides the required functionality.

### Prefer interfaces to reflection

Reflection allows one class to use another, even if the latter class did not exist when the former was compiled. This comes at a price:

* You lose all the benefits of compile-type type checking.
* The code required to perform reflective access is clumsy and verbose.
* Performance suffers.

You can obtain many of the benefits of reflection while incurring few of its costs by using it in a very limited form. Create instances reflectively and access them normally via their interface or superclass.

Reflective instantiation with interface access.

```java
public static void main(String[] args) {
    // Translate the class name into a Class object
    Class<? extends Set<String>> cl = null;
    try {
        cl = (Class<? extends Set<String>>)  // Unchecked cast!
                Class.forName(args[0]);
    } catch (ClassNotFoundException e) {
        fatalError("Class not found.");
    }
    // Get the constructor
    Constructor<? extends Set<String>> cons = null;
    try {
        cons = cl.getDeclaredConstructor();
    } catch (NoSuchMethodException e) {
        fatalError("No parameterless constructor");
    }
    // Instantiate the set
    Set<String> s = null;
    try {
        s = cons.newInstance();
    } catch (IllegalAccessException e) {
        fatalError("Constructor not accessible");
    } catch (InstantiationException e) {
        fatalError("Class not instantiable.");
    } catch (InvocationTargetException e) {
        fatalError("Constructor threw " + e.getCause());
    } catch (ClassCastException e) {
        fatalError("Class doesn't implement Set");
    }
    // Exercise the set
    s.addAll(Arrays.asList(args).subList(1, args.length));
    System.out.println(s);
}
private static void fatalError(String msg) {
    System.err.println(msg);
    System.exit(1);
}
```

### Use native methods judiciously

The Java Native Interface (JNI) allows Java programs to call _native methods_ written in _native programming languages_ such as C or C++.

It is rarely advisable to use native methods for improved performance.

### Optimise judiciously

Strive to write good programs rather than fast ones.

Strive to avoid design decisions that limit performance.

Consider the performance consequences of your API design decisions.

It is a very bad idea to warp an API to achieve good performance. The performance issue that caused you to warp the API may go away in a future.

Measure performance before and after each attempted optimisation.

### Adhere to generally accepted naming conventions

Package and module names should be hierarchical, with components separated by periods. Alphabetic characters, rarely digits.

Components should be short, meaningful abbreviations or acronyms.

Class and interface names, including enum and annotation type names, should consist of one or more words, with the first letter of each word capitalised. Abbreviations should be avoided. If you use acronyms, capitalise just the first letter. Better to have `HttpUrl` than `HTTPURL`.

Method and field names follow the same conventions as before, except that first letter should be lowercase.

Constant fields should consist of one or more upper case words separated by the underscore character.

Local variable names have similar conventions to member names, except that abbreviations are permitted.

Type parameters consist of a single letter. `T` for arbitrary type `E` for element type, `K` and `V` for key and value types of a map, and `X` for exception. Return type is usually `R`. A sequence of arbitrary types can be `T`, `U`, `V` or `T1`, `T2`, `T3`.

Instantiable classes, including enum types are generally named with a singular noun or noun phrase.

Non instantiable utility classes are often named with a plural noun or with an adjective ending in `able` or `ible`. In case of annotations, nouns, verbs, prepositions and adjectives are all common.

Methods that perform some action are generally named with a verb or verb phrase. Methods that return a `boolean` value usually have names that begin with the word `is` or `has` followed by a noun, noun phrase that functions as an adjective.

Method that return non-`boolean` attribute of the object are usually named with a noun, a noun phrase or a verb phrase beginning with the verb `get`, although nowadays might not be necessary.

Instance methods that convert the type of a n object, are often called `to`_`Type`_. Methods that return a view whose type differs from that of receiving object are often called as `as`_Type_. Methods that return a primitive with the same value as the object on which they're invoked are often called _type_`Value`.

Fields of type `boolean` are often named like `boolean` accessor methods with the initial `is` omitted. Fields of other types are usually named with nouns or noun phrases.

## Exceptions

### Use exceptions for exceptional conditions

Horrible abuse of exceptions

```java
try {
    int i = 0;
    while(true)
        range[i++].climb();
} catch (ArrayIndexOutOfBoundsException e) {
}
```

* Exception processing is slow
* Placing code into a `try-catch` block inhibits some optimisations the JVM perform

Exceptions should never be used for ordinary control flow.

A well-designed API must not force its clients to use exceptions for ordinary control flow.

### Use checked exceptions for recoverable conditions and runtime exceptions for programming errors

Use checked exceptions for conditions from which the caller can reasonably be expected to recover.

Use runtime exceptions to indicate programming errors. _Precondition violations_ or the failure by the client of an API to adhere to the contract established by the API specification.

`Error` exceptions are usually intended for the JVM  to indicate conditions that make it impossible to continue execution. Therefore **all of the unchecked throwables you implement should subclass `RuntimeException`.** You shouldn't throw `Error` exceptions either.

Exceptions are full-fledged objects, define methods to provide additional information concerning the condition that caused the exception. This is crucial for checked exceptions.

### Avoid unnecessary use of checked exceptions

Checked exceptions _force_ programmers to deal with problems. Overuse of checked exceptions can make them far less pleasant to use.

### Favour the use of standard exceptions

Do not reuse `Exception`, `RuntimeException`, `Throwable` or `Error` directly.

Most commonly reused exceptions

Exception                         | Occasion for use
----------------------------------|-----------------
`IllegalArgumentException`        | Non-null parameter value is inappropriate
`IllegalStateException`           | Object state is inappropriate for method invocation
`NullPointerException`            | Parameter value is null where prohibited
`IndexOutOfBoundsException`       | Index parameter value is out of range
`ConcurrentModificationException` | Concurrent modification of an object has been detected where it is prohibited
`UnsupportedOperationException`   | Object does not support method

Throw `IllegalStateException` if no argument values would have worked, otherwise throw `IllegalArgumentException`.

### Throw exceptions appropriate to the abstraction

Higher layers should catch lower-level exceptions and, in their place, throw exceptions that can be explained in terms of the higher-level abstraction.

Exception translations

```java
try {
   ... // Use lower-level abstraction to do our bidding
} catch (LowerLevelException e) {
   throw new HigherLevelException(...);
}
```

Sometimes the low-level exception might be helpful to someone debugging the higher-level.

_Exception chaining_

```java
try {
    ... // Use lower-level abstraction to do our bidding
} catch (LowerLevelException cause) {
    throw new HigherLevelException(cause);
}
```

While exception translation is superior to mindless propagation of exceptions from lower layers, it should not be overused. The best way to deal with exceptions from lower layers is to avoid them, by ensuring that lower-level methods succeed. Sometimes you can do this by checking the validity of parameters to be passed to lower level abstractions.

### Document all exceptions thrown by each method

Always declare checked exceptions individually, and document precisely the conditions under which each one is thrown.

Use the Javadoc `@throws` tag to document each exception that a method can throw, but do not use the `throws` keyword on unchecked exceptions.

If an exception is thrown by many methods in a class for the same reason, you can document the exception in the class's documentation comment.

### Include failure-capture information in detail messages

**To capture a failure, the detail message of an exception should contain the values of all parameters and fields that contributed to the exception.** For example `IndexOutOfBoundsException` should contain the lower bound, the upper bound, and the index value that failed.

Do not include passwords, encryption keys, and the like in detail messages as stack traces may be seen by many people diagnosing and fixing software issues.

One way to ensure that exceptions contain adequate failure-capture information in their detail messages is to require this information in their constructors.

### Strive for failure atomicity

Generally speaking, a failed method invocation should leave the object in the state that it was in prior the invocation.

The simplest way is to design immutable objects, where failure atomicity is free.

For methods that operate on mutable objects, the most common way to achieve failure atomicity is to check parameters for validity before performing the operation.

### Don't ignore exceptions

An empty `catch` block defeats the purpose of exceptions.

```java
try {
    ...
} catch (SomeException e) {
}
```

If you choose to ignore an exception, the `catch` block should contain a comment explaining why it is appropriate to do so and the variable should be named `ignored`.

```java
Future<Integer> f = exec.submit(planarMap::chromaticNumber);
int numColors = 4; // Default; guaranteed sufficient for any map
try {
    numColors = f.get(1L, TimeUnit.SECONDS);
} catch (TimeoutException | ExecutionException ignored) {
    // Use default: minimal coloring is desirable, not required
}
```

## Concurrency

### Synchronise access to shared mutable data

Synchronisation is required for reliable communication between threads as well as for mutual exclusion.

Do not use `Thread.stop` as it is inherently _unsafe_, its use can result in data corruption.

Broken

```java
public class StopThread {
    private static boolean stopRequested;

    public static void main(String[] args)
            throws InterruptedException {
        Thread backgroundThread = new Thread(() -> {
            int i = 0;
            while (!stopRequested)
                i++;
        });
        backgroundThread.start();

        TimeUnit.SECONDS.sleep(1);
        stopRequested = true;
    }
}
```

Properly synchronised cooperative thread termination

```java
public class StopThread {
    private static boolean stopRequested;

    private static synchronized void requestStop() {
        stopRequested = true;
    }

    private static synchronized boolean stopRequested() {
        return stopRequested;
    }

    public static void main(String[] args)
            throws InterruptedException {
        Thread backgroundThread = new Thread(() -> {
            int i = 0;
            while (!stopRequested())
                i++;
        });
        backgroundThread.start();

        TimeUnit.SECONDS.sleep(1);
        requestStop();
    }
}
```

Synchronisation is not guaranteed to work unless both read and write operations are synchronised.

Either share immutable data, or don't share at all. Confine mutable data into a single thread.

When multiple threads share mutable data, each thread that reads or writes the data must perform synchronisation.

### Avoid excessive synchronisation

To avoid liveness and safety failures, never cede control to the client within a synchronised method or block. Inside a synchronised region, do not invoke a method that is designed to be overridden, or one provided by a client in the form a function object.

As a rule, you should do as little work as possible inside synchronised regions.

### Prefer executors, tasks, and streams to threads

```java
ExecutorService exec = Executors.newSingleThreadExecutor();
```

```java
exec.execute(runnable);
```

```java
exec.shutdown();
```

You should refrain from working directly with threads, a `Thread` serves as both a unit of work and the mechanism for executing it. In the executor framework, the unit of work and the execution are separate.

### Prefer concurrency utilities to `wait` and `notify`

Given the difficulty of using `wait` and `notify` correctly, you should use the higher-level concurrency utilities instead.

It is impossible to exclude concurrent activity from a concurrent collection; locking it will only slow the program.

Use `ConcurrentHashMap` in preference to `Collections.synchronizedMap`. Doing so can dramatically increase the performance of concurrent applications.

For interval timing, always use `System.nanoTime` rather than `System.currentTimeMillis`. `System.nanoTime` is more accurate and is unaffected by adjustments to the system's real-time clock.

The standard idiom for using `wait` method

```java
synchronized (obj) {
    while (<condition does not hold>)
        obj.wait(); // (Releases lock, and reacquires on wakeup)
    ... // Perform action appropriate to condition
}
```

Always use the wait loop idiom to invoke the `wait` method; never invoke it outside of a loop. The loop serves to test the condition before and after waiting.

There is seldom, if ever, a reason to use `wait` and `notify` in new code.

### Document thread safety

The presence of `synchronized` modifier in a method declaration is an implementation detail, not a part of its API.

To enable safe concurrent use, a class must clearly document what level of thread safety it supports:
* **Immutable.** No extra synchronisation is necessary.
* **Unconditionally thread-safe.** Instances are mutable, but clients don't need to worry about synchronisation.
* **Conditionally thread-safe.** Instances are mutable. Some methods require external synchronisation for safe concurrent use.
* **Not thread-safe.** Instances are mutable, clients must surround each method invocation with external synchronisation.
* **Thread-hostile.** The class is unsafe for concurrent use even if every method invocation is surrounded by external synchronisation.

Lock fields should always be declared `final`.

### Use lazy evaluation judiciously

Under most circumstances, normal initialisation is preferable to lazy initialisation.

Normal initialisation of an instance field

```java
private final FieldType field = computeFieldValue();
```

If you use lazy initialisation to break an initialisation circularity, use a synchronised accessor.

```java
private FieldType field;

private synchronized FieldType getField() {
    if (field == null)
        field = computeFieldValue();
    return field;
}
```

If you need to use lazy initialisation for performance on a static field, use the lazy initialisation holder class idiom.

```java
private static class FieldHolder {
    static final FieldType field = computeFieldValue();
}

private static FieldType getField() { return FieldHolder.field; }
```

If you need to use lazy initialisation for performance on an instance field, use the double-check idiom.

```java
private volatile FieldType field;

private FieldType getField() {
    FieldType result = field;
    if (result == null) {  // First check (no locking)
        synchronized(this) {
            if (field == null)  // Second check (with locking)
                field = result = computeFieldValue();
        }
    }
    return result;
}
```

### Don't depend on thread scheduler

Any program that relies on the thread scheduler for correctness or performance is likely to be nonportable.

Threads should not run if they aren't doing useful work.

Awful `CountDownLatch` implementation, busy-waits incessantly.

```java
public class SlowCountDownLatch {
    private int count;

    public SlowCountDownLatch(int count) {
        if (count < 0)
            throw new IllegalArgumentException(count + " < 0");
        this.count = count;
    }

    public void await() {
        while (true) {
            synchronized(this) {
                if (count == 0)
                    return;
            }
        }
    }

    public synchronized void countDown() {
        if (count != 0)
            count--;
    }
}
```

Resist the temptation to "fix" the program by putting calls to `Thread.yield`, it depends a lot on the JVM and it has no testable semantics.

Thread semantics are among the least portable features of Java.

## Serialisation

### Prefer alternatives to Java serialisation

The best way to avoid serialisation exploits is never to deserialise anything. There is no reason to use Java serialisation in any new system you write.

If you can't avoid serialisation, your next best alternative is to never deserialise untrusted data.

You can use the objet deserialisation filter added in Java 9 `java.io.ObjectInputFilter`. Accepting classes by default and rejecting a list of potentially dangerous ones is know as _blacklisting_; rejecting classes by default and accepting a list of those that are presumed safe is know as _whitelisting_. **Prefer whitelisting to blacklisting**.

### Implement `Serializable` with great caution

A major cost of implementing `Serializable` is that it decreases the flexibility to change a class's implementation once it has been released, it's byte-stream encoding becomes part of its exported API.

A second cost of implementing `Serializable` is that it increases the likelihood for bugs and security holes.

A third cost of implementing `Serializable` is that it increases the testing burden associated with releasing a new version of a class. It is important to check that it is possible to serialise an instance in the new release and deserialise it in old releases, and vice versa.

Implementing `Serializable` is not a decision to be undertake lightly.

Classes designed for inheritance should rarely implement `Serializable`, and interfaces should rarely extend it. Doing so would place substantial burden on anyone who extends the class or implements the interface.

Inner classes should not implement `Serializable`. The default serialised form of an inner class is ill-defined precisely because of the _enclosed instances_. A _static member class_ can however, implement `Serializable`.

### Consider using a custom serialised form

Do not accept the default serialised form without first considering whether it is appropriate, you'll never escape completely from the implementation.

The default serialised form is likely to be appropriate if an object's physical representation is identical to its logical content.

A good candidate for default serialised form

```java
public class Name implements Serializable {
    /**
     * Last name. Must be non-null.
     * @serial
     */
    private final String lastName;

    /**
     * First name. Must be non-null.
     * @serial
     */
    private final String firstName;
    /**
     * Middle name, or null if there is none.
     * @serial
     */
    private final String middleName;

    ... // Remainder omitted
}
```

Even if you decide that the default serialised form is appropriate, you often must provide a `readObject` method to ensure invariants and security.

An awful candidate for default serialised form.

```java
public final class StringList implements Serializable {
    private int size = 0;
    private Entry head = null;

    private static class Entry implements Serializable {
        String data;
        Entry  next;
        Entry  previous;
    }

    ... // Remainder omitted
}
```

Using a default serialised form when an object's physical representation differs substantially from its logical data content has four advantages.

* It permanently ties the exported API to the current internal representation.
* It can consume excessive space.
* It can consume excessive time.
* It can cause stack overflows.

`StringList` with a reasonable custom serialised form.

```java
public final class StringList implements Serializable {
    private transient int size   = 0;
    private transient Entry head = null;

    // No longer Serializable!
    private static class Entry {
        String data;
        Entry  next;
        Entry  previous;
    }

    // Appends the specified string to the list
    public final void add(String s) { ... }

    /**
     * Serialize this {@code StringList} instance.
     *
     * @serialData The size of the list (the number of strings
     * it contains) is emitted ({@code int}), followed by all of
     * its elements (each a {@code String}), in the proper
     * sequence.
     */
    private void writeObject(ObjectOutputStream s)
            throws IOException {
        s.defaultWriteObject();
        s.writeInt(size);

        // Write out all elements in the proper order.
        for (Entry e = head; e != null; e = e.next)
            s.writeObject(e.data);
    }

    private void readObject(ObjectInputStream s)
            throws IOException, ClassNotFoundException {
        s.defaultReadObject();
        int numElements = s.readInt();

        // Read in all elements and insert them in list
        for (int i = 0; i < numElements; i++)
            add((String) s.readObject());
    }

    ... // Remainder omitted
}
```

Every instance field that isn't labeled `transient` will be serialised within the `defaultWriteObject` method is invoked. Every instance field that can be declared transient, should be. Before deciding to make a field nontransient, convince yourself that its value is part of the logical state of the object.

You must impose any synchronisation on object serialisation that you would impose on any other method that reads the entire state of the object.

```java
private synchronized void writeObject(ObjectOutputStream s)
        throws IOException {
    s.defaultWriteObject();
}
```

Regardless of what serialised form you choose, declare an explicit serial version UID in every serialisable class you write. This eliminates the serial version UID in every serialisable class you write, plus it has some performance benefits.

```java
private static final long serialVersionUID = randomLongValue;
```

It doesn't matter what value you choose.

If you ever want to make a new version of a class that is _incompatible_ with existing versions, merely change the value in the serial version UID declaration. Do not change the serial version UID unless you want to break compatibility with all existing serialised instances of a class.

### Write `readObject` methods defensively

When an object is deserialised, it is critical to defensively copy any field containing an object reference that a client must not possess.

`readObject` method with defensive copying and validity checking.

```java
private void readObject(ObjectInputStream s)
        throws IOException, ClassNotFoundException {
    s.defaultReadObject();

    // Defensively copy our mutable components
    start = new Date(start.getTime());
    end   = new Date(end.getTime());

    // Check that our invariants are satisfied
    if (start.compareTo(end) > 0)
        throw new InvalidObjectException(start +" after "+ end);
}
```

* For classes with object reference fields that must remain private, defensively copy each object in such a field. Mutable components of immutable classes fall into this category.
* Check any invariants and throw an `InvalidObjectException` if a check fails. The checks should follow any defensive copying.
* If an entire object graph must be validated after it is deserialised, use the `ObjectInputValidation` interface.
* Do not invoke any overridable methods in the class, directly or indirectly.

### For instance control, prefer enum types to `readResolve`

```java
public class Elvis {
    public static final Elvis INSTANCE = new Elvis();

    private Elvis() {  ... }

    public void leaveTheBuilding() { ... }
}
```

`readResolve` for instance control, you can do better!

```java
private Object readResolve() {
    // Return the one true Elvis and let the garbage collector
    // take care of the Elvis impersonator.
    return INSTANCE;
}
```

If you depend on `readResolve` for instance control, all instance field with object reference types myst be declared `transient`. An attacker might secure a reference to the deserialised object before its `readResolve` method is run.

Broken singleton, has nontransient object reference field.

```java
public class Elvis implements Serializable {
    public static final Elvis INSTANCE = new Elvis();
    private Elvis() { }

    private String[] favoriteSongs =
        { "Hound Dog", "Heartbreak Hotel" };
    public void printFavorites() {
        System.out.println(Arrays.toString(favoriteSongs));
    }

    private Object readResolve() {
        return INSTANCE;
    }
}
```

Enum singleton, the preferred approach.

```java
public enum Elvis {
    INSTANCE;
    private String[] favoriteSongs =
        { "Hound Dog", "Heartbreak Hotel" };
    public void printFavorites() {
        System.out.println(Arrays.toString(favoriteSongs));
    }
}
```

The accessibility of `readResolve` is significant. On final classes, it should be private. On nonfinal class, you must carefully consider its accessibility.

### Consider serialisation proxies instead of serialised instances

Making classes implement `Serializable` increases the likelihood of bugs and security problems as it allows instances to be created using extralinguistic mechanism in place of ordinary constructors. There is a technique that greatly reduces the risks called _serialisation proxy pattern_.

Serialisation proxy for `Period` class

```java
private static class SerializationProxy implements Serializable {
    private final Date start;
    private final Date end;

    SerializationProxy(Period p) {
        this.start = p.start;
        this.end = p.end;
    }

    private static final long serialVersionUID =
        234098243823485285L; // Any number will do (Item  87)
}
```

`writeReplace` method for the serialisation proxy pattern

```java
private Object writeReplace() {
    return new SerializationProxy(this);
}
```

`readObject` method for the serialisation proxy pattern

```java
private void readObject(ObjectInputStream stream)
        throws InvalidObjectException {
    throw new InvalidObjectException("Proxy required");
}
```

`readResolve` method for `Period.SerializationProxy`

```java
private Object readResolve() {
    return new Period(start, end);    // Uses public constructor
}
```

Consider the serialisation proxy pattern whenever you find yourself having to write a `readObject` or `writeObject` method on a class not extendable by its clients. This pattern is perhaps the easiest way to robustly serialise object with nontrivial invariants.
