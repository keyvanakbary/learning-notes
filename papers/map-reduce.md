# [MapReduce: Simplified Data Processing on Large Clusters](https://static.googleusercontent.com/media/research.google.com/en//archive/mapreduce-osdi04.pdf)

MapReduce is a programming model and an associated implementation for processing and generating large data sets. Users specify a _map_ function that processes a key/value pair to generate a set of intermediate key/value pairs, and a _reduce_ function that merges all intermediate values associated with the same intermediate key.

Programs written in this functional style are automatically parallelised and executed on a large cluster of commodity machines. The run-time system takes care of the details of partitioning the input data, scheduling the program's execution across a set of machines, handling machine failures, and managing the required inter-machine communication. This allows programmers without any experience with parallel and distributed systems to easily utilise the resources of a large distributed system.

## Introduction

The abstraction is inspired by the _map_ and _reduce_ primitives present in Lisp and many other functional languages. Map and reduce operations allows easy parallelisation at the same time that re-execution serves as the primary mechanism for fault-tolerance.

## Programming model

The computation takes a set of _input_ key/value pairs, and produces a set of _output_ key/value pairs. The user of the MapReduce library expresses the computations as two functions: _Map_ and _Reduce_.

_Map_, written by the user, takes an input pair and produces a set of _intermediate_ key/value pairs. The MapReduce library groups together all intermediate values associated with the same intermediate Key _I_ and passes them to the _Reduce_ function.

The _Reduce_ function, also written by the user, accepts and intermediary key _I_ and a set of values for that key. It merges together these values to form a possibly smaller set of values. Typically just zero or one output value is produced per _Reduce_ invocation.

### Usage exmples

* Distributed Grep: The map function emits a line if it matches a supplied pattern. The reduce function is an identity function that just copies the supplied intermediate data to the output.
* Count of URL access frequency: The map function processes logs of a web page requests and outputs `<URL, 1>`. The reduce function adds together all values for the same URL and emits a `<URL, total count>` pair.
* Distributed sort: The map functions extracts the key from each record, and emits a `<key, record>` pair. The reduce function emits all pairs unchanged.

## Implementation

One implementation may be suitable for a small shared-memory machine, another for a large NUMA multi-processor, and yet another for an even larger collection of networked machines.

### Execution overview

The _Map_ invocations are distributed across multiple machines by automatically partitioning the input data into a set of _M splits_. The input splits can be processed in parallel by different machines. _Reduce_ invocations are distributed by partitioning the intermediate key space into _R_ pieces using a partitioning function. The number of partitions (_R_) and the partitioning function are specified by the user.

Overall flow:
1. The MapReduce library in the user program **splits the input files into _M_ pieces** typically 16MB per piece. It then starts up many copies of the program on a cluster of machines.
2. One of the copies of the program is special, the master. The rest are workers that are assigned work by the master. There are _M_ map tasks and _R_ reduce tasks to assign. **The master picks idle workers and assigns each one a map task or reduce task.**
3. A worker who is assigned a map task reads the contents of the corresponding input split. It **parses key/value pairs out of the input data and passes each pair to the user-defined _Map_** function. The intermediate key/value pairs produced by the _Map_ function are buffered in memory.
4. Periodically, the **buffered pairs are written to local disk**, partitioned into _R_ regions by the partitioning function. The locations of these buffered pairs on the local disk are passed back to the master, who is responsible for forwarding these locations to the reduce workers.
5. When a **reduce worker** is notified by the master about these locations, it **uses remote procedure calls to read the buffered data from the local disks of the map workers**. When a reduce worker has read all intermediate data, it sorts it by the intermediate keys so that all occurrences of the same key are grouped together.
6. The **reduce worker** iterates over the sorted intermediate data and **for each unique intermediate key encountered, it passes the key and the corresponding set of intermediate values to the user's _Reduce_ function**. The output of the _Reduce_ function is appended to a final output file for this reduce partition.
7. When all map tasks and reduce tasks have been completed, the master wakes up the user program. At this point the MapReduce call in the user program returns back to the user code.

After successful completion, the output of the MapReduce execution is available in the _R_ output files (one per reduce task, with the file names as specified by the user). Users usually don't need to combine these _R_ output files into one file, they can either use another MapReduce call or use a distributed application to process them.

### Master data structures

For each map task and reduce task, master stores the state (_idle_, _in-progress_, or _completed_) and the identity of the worker machine.

For each completed map task, the master stores the locations and sizes of the _R_ intermediate file regions produced by the map task. Updates to this location and size information are received as map tasks are compelted. The information is pushed incrementally to workers that have _in-progress_ reduce tasks.

### Fault tolerance

#### Worker failure

The master pings every worker periodically. If no response is received from a worker in a certain amount of time, the master marks the worker as failed. Any map tasks completed by the worker are reset back to their initial _idle_ state, and therefore  become eligible for scheduling on other workers. Similarly, any map task or reduce task in progress on a failed worker is also reset to _idle_ and becomes eligible for rescheduling.

Completed map tasks are re-executed on failure because their output is stored on the local disks of the failed machine and is therefore inaccessible. Completed reduce tass do not need to be re-executed since their output is stored in a global file system.

When a map task is executed first by worker _A_, and later executed by worker _B_ (because _A_ failed), all workers executing reduce tasks are notified of the re-execution. Any reduce task that has not already read the data from worker _A_ will read the data from worker _B_.

The MapReduce master simply re-executes the work done by unreachable worker machines and continues to make forward progress.

#### Master failure

It's easy to make the master write periodic checkpoints of the master data structures. If the master task dies, a new copy can be started from the last checkpointed state. Current implementation aborts the MapReduce computation if the master fails.

#### Semantics in the presence of failures

The vast majority of _map_ and _reduce_ operators are deterministic, and the fact that the semantics are equivalent to a sequential execution in this case makes it very easy for programmers to reason about their program's behaviour.

### Localty

Network bandwith can be conserved by taking advantage of the fact that the input data (managed by GFS) is stored on the local disks of the machine that make up the cluster. Most input data is read locally and consumes no network bandwidth.

### Task granularity

The map phase is subdivided into _M_ pieces and reduce phase is divided into _R_ Pieces. Having each worker perform many different tasks improves dynamic load balancing and also speeds up recovery when a worker fails.

### Backup tasks

One of the common causes that lengthens the total time taken for a MapReduce operation is a "straggler", a machine that takes an unusually long time to complete one of the last few map or reduce tasks in the computation.

There is a general mechanism to alleviate the problem of stragglers. When a MapReduce operation is close to completion, the master schedules backup executions of the remaining _in-progress_ tasks. The task is marked as completed whenever either the primary or the backup execution completes. A distributed sorting program can take up to 44% longer without the backup task mechanism.

## Refinement

### Partitioning function

Users of MapReduce specify the number of reduce task/output files that they desire (_R_). A default partitioning function is provided that uses hashing (peg: `hash(key) mod R`), which tends to result in fairly well-balanced partitions. In some cases, it is useful to partition data by some other function of the key, for example sometimes the output keys are URLs, and is convenient to have a single host end up in the same output file. A partitioning function can be provided to MapReduce, for example `hash(Hostname(urlkey)) mod R`.

### Ordering guarantees

Within a given partition, the intermediate key/value pairs are guaranteed to be processed in increasing key order, which makes it easy to generate a sorted output file per partition.

### Combiner function

MapReduce allows the user to specify a _Combiner_ function that does partial merging of the data before it is sent over the network.

The _Combiner_ function is executed on each machine that performs a map task. The difference between a reduce function and a combiner function is how the MapReduce library handles the output of the function. The output of a reduce function is written to the final output file. The output of a combiner function is written to an intermediate field that will be sent to a reduce task.

### Input and output types

"Text" mode input treats each line as a key/value pair: the key is the offset in the file and the value is the contents of the line. Another common supported format stores a sequence of a key/value pairs sorted by key.

Users can add support for a new input type by providing an implementation of a simple _reader_ interface, though most users just use one of a small number of predefined input types.

In a similar fashion, a set of output types for producing data in different formats is supported.

### Side-effects

Users of MapReduce may find convenient to produce auxiliary files. The application writer can make such side-effects atomic and idempotent.

### Skipping bad records

Sometimes there are bugs in user code that can cause the _Map_ or _Reduce_ functions to crash deterministically on certain records, which prevents the whole MapReduce operation from completing.

There is an optional mode of execution where the MapReduce library detects which records cause deterministic crashes and skips these records in order to make forward progress. Each worker process installs a signal handler that catches segmentation violations and bus errors. Before invoking a user _Map_ or _Reduce_ operation, the MapReduce library stores the sequence number of the argument in a variable. The signal handler sends a "last gasp" UDP packet that contains the sequence number to the master. When the master has seen more than one failure on a particular record, it indicates that the record should be skipped.

### Local execution

To help facilitate debugging, profiling, and small-scale testing, there is an alternative implementation of the MapReduce library that sequentially executes all of the work for a MapReduce operation on the local machine.

### Status information

The master runs an internal HTTP server and exports a set of status pages for human consumption.

### Counters

The MapReduce library provides a counter facility to count occurrences of various events, like the count of total number of words processed, documents indexed, etc.

The counter values from individual worker machines are periodically propagated to the master. The master aggregates the counter values from successful map and reduce tasks and returns them to the user code when the MapReduce operation is completed. The master eliminates the effects of duplicate executions of the same map or reduce task to avoid double counting.

## Experience

MapReduce has been used at Google for a wide range of domains including:

* Large-scale machine learning problems.
* Clustering problems for the Google News and Froggle products.
* Extraction of data used to produce reports of popular queries.
* Extraction of the properties of web pages for new experiments and products.
* Large-scale graph computations.

MapReduce has been so successful because it makes it possible to write a simple program and run it efficiently on a thousand machines int he course of half an hour, greatly speeding up the development and prototyping cycle. It allows programmers who have no experience with distributed and/or parallel systems to exploit large amounts of resources easily.

### Large-scale indexing

Probably the most significant use of MapReduce is the rewrite of the production indexing system that produces the data structures used for the Google web search service. Using MapReduce has provided several benefits:

* The indexing code is simpler, smaller, and easier to understand, because the code that deals with fault tolerance, distribution, and parallelisation is hidden within the MapReduce library.
* The performance of the MapReduce library is good enough that it can keep conceptually unrelated computations separate, instead of mixing them together to avoid extra passes over the data.
* The indexing process has become much easier to operate, because most of the problems caused by machine failures, slow machines, and networking hiccups are dealt with automatically by the MapReduce library without operator intervention.

## Related work

MapReduce exploits a restricted programming model to parallelise the user program automatically and to provide transparent fault-tolerance.

By restricting the programming model, the MapReduce framework is able to partition the problem into a larger number of fine-grained tasks. These tasks are dynamically scheduled on available workers so that faster worker process more tasks. The restricted programming model also allows to schedule redundant execution of tasks near the end of the job which greatly reduces completion time in the presence of non-uniformities.

## Conclusions

The success of MapReduce is attributed to:
1. The model is easy to use, even for programmers without experience with parallel and distributed systems, since it hides the details of parallelisation, fault-tolerance, locality optimisation, and load balancing.
2. A large variety of problems are easily expressible as MapReduce computations.
3. There is an implementation of MapReduce that scales to large clusters of machines compromising thousand of machines.

Some learnings:
1. Restricting the programming model makes it easy to parallelise and distribute computations and to make such computations fault-tolerance.
2. Network bandwidth is a scarce resource. A number of optimisations in the system have been done towards reducing the amount of data sent across the network.
3. Redundant execution can be used to reduce the impact of slow machines, and to handle machine failures and data loss.