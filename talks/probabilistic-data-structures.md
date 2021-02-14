# [Probabilistic Data Structures](https://www.youtube.com/watch?v=F7EhDBfsTA8)

They allow you to do things in memory at scale for things you couldn't do before with a very tiny memory footprint.

Something you have to know is that you as a developer is that you have to accept a predictable level of inaccuracy.

## Bloom filters

For working out if something is in a set.

With Java, a naive implementation could be using a `Set`.

The problem is if we start adding loads of stuff into a `Set`. Insertion time gets slower, heap space in JVM get massive.

[Space/Time Trade-offs in Hash Coding with Allowable Errors paper](http://crystal.uta.edu/~mcguigan/cse6350/papers/Bloom.pdf)

Parts of a Bloom filter:
* A bit array of size _n_
* _k_ hash functions

A Bloom filter can tell you if something is not there, and _maybe_ if is there.

Available in Google Guava library `com.google.guava:guava:19.0` as `BloomFilter`. There is an error rate of checking existence in the set. Adjusting this error size, affects insertion performance. The more accurate you want to be, the more hash functions you have.

Use cases:
* "One hit wonders" If you visit a page once, content for you will be served from a Bloom filter. For any other case, we can serve you something more computationally expensive.
* Avoiding lookups (HBase, Cassandra)
* Real-time matching, real-time searches.

## Count-min sketch

Slightly newer than Bloom filters. Similar use case, for checking membership. More used for count tracking (how many times something exists).

If you were using a naive Java implementation for the problem, you can use a `HashMap`, or a `HashMultiset` (a `HashMap` with a key for the element, and an integer as a value counter).

Same issues as before, insertion time and heap size gets bigger.

[Approximating Data with the Count-Min Data Structure paper](http://dimacs.rutgers.edu/~graham/pubs/papers/cmsoft.pdf).

Initialising a sketch:
* Epsilon: accepted error added to counts with each item.
* Delta: Probability that estimate is outside accepted error.

You can use `com.clearspring.analytics:stream:2.9.2` and `CountMinSketch`.

Use cases:
* Any kind of frequency tracking!
* Natural Language Processing
* Extension: Heavy-hitters
* Extension: Range-query

## HyperLogLog

Is used for cardinality, "in my list of things, how many unique items are there". "What are my unique visitors to my site today".

Naively in Java we can do it with a Set again. Just retrieving back the unique elements inserted (not-repeated). `mySet.size()`.

This is an implementation of a compound of papers:
* Linear counting, similar to Bloom filter: [A Linear-Time Probabilistic Counting Algorithm for Database Applications paper](http://dblab.kaist.ac.kr/Publication/pdf/ACM90_TODS_v15n2.pdf)
* LogLog counting: [Loglog Counting of Large Cardinalities paper](http://algo.inria.fr/flajolet/Publications/DuFl03-LNCS.pdf)
* HyperLogLog: [HyperLogLog: the analysis of a near-optimal cardinality estimation algorithm paper](http://algo.inria.fr/flajolet/Publications/FlFuGaMe07.pdf)

You can use `com.clearspring.analytics:stream:2.9.2` and `HyperLogLog`.

Use cases:
* Anywhere you need cardinality in O(n)!
* Unique site visitors
* Estimates of massive tables
* Streams of data