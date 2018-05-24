Java Collections
===================

### Collection
* Parameterized interface that represents generalized grouping of object
* Specified methods - adding, removing, testing object for membership, iterating, return elements as an array, return the size of the collection
* **Set**
  * It doesn’t allow duplicates. Otherwise nothing really special
  * **HashSet** - represent by hash table
  * **TreeSet** - implements SortedSet, it is [red-black tree](https://en.wikipedia.org/wiki/Red%E2%80%93black_tree)
  * **LinkedHashSet** - keeps order, hash table
  * EnumSet - only enum values
  * CopyOnWriterArraySet - thread safe without synchronized methods, implemented as array  
* **List**
  * Each element of the list has position or index. It is similar as Array but size can be changed.
  * **LinkedList** - needs more memory than ArrayList (double-linked list). It is efficient for working with beginning and end of the list but inefficient for random access. Good for adding and removing elements.
  * **ArrayList** - array allocate more 1.5x more space when it is full
  * CopyOnWriteArrayList - thread safe, fast traversal, slow modification
  * Vector - just legacy (Java 1.0) -> should not be used
  * Stack - legacy, extends Vector, use Deque instead!  
* **Queue & BlockingQueue**
  * It has fixed capacity. It is possible to access only first element
  * **PriorityQueue**: needs comparator
  * **ArrayDeque**: can be used as stack
  * Methods: `add()`, `offer()`, `put()`, `remove()`, `poll()`, `take()`
### Map:
* It is the interface and does **not implement Collection** interface
* It is a set of key objects that map value object
* Methods: `put()`, `get()`, `remove()`, `isEmpty()`, `size()`
* **HashMap** - we can not be sure about an order that objects will be iterated. careful about method hashCode()
* **TreeMap** - is sorted Map according method comapreTo() or class Comparator. Implemented interface SortedMap
* **LinkedHashMap** - elements are iterated in same order as they were inserted
* EnumMap - represented as array
* ConcurentHashMap - thread safe implementation, (`ConcurrentMap` interface)
### Iterator & Iterable
If object/collection implements Iterable, it means that it has method `iterator()` which return an iterator that can loop through objects in the collection.
### Comparable & Comparator
### Arrays & Collections
Classes contain static util methods for a work with Array/Collection

## Lambda Expressions
* They are anonymous functions that are not associated with a class and can be treated as value
* Can be used whenever the type is a functional interface ([single abstract method, SAM](https://stackoverflow.com/a/17913661/5826090)). It provides the implementation of the abstract method.  
* **Lambda expression should satisfy:**
  * Lambda must appear where an i**nstance of an interface** (@FunctionalInterface) type **is expected**
  * Expected interface type should have exactly **one mandatory method** (single non-default method)
  * Expected interface method should have a **signature** that **exactly matches** that of Lambda expression
* Variable in the surrounding scope can be used in a Lambda expression, but they must be either final or effectively final
* **Method** (static or instance) **reference**: `target_reference::method_name` 
* `Consumer<T>` takes single value and returns nothing
* `Supplier` is opposite to Consumer
* `Function<T, R>` accepts one argument and returns one
* `UnaryOperator<T>` is specialized form of function
* `BinaryOperator<T>` is specialized form of BiFuntion
* `Predicate<T>` is boolean-value function of one argument

## Streams
* New **lazy evaluated** abstraction of the `Collection`. It has a similar role to `Iterator`.
* It can be generated from collection via `stream()` method
* Sequence of operator (pipeline) can be applied to the collection
* The result needs to be gathered back into collection on the end of pipeline. We can use `Collector` or terminal method as `reduce()`
* Streams supports parallel access - **multithreaded way**
* Streams do not manage storage for data. It is possible to build infinite stream but `collect()` won’t work for them.
* **Filter** accepts an instance of `Predicate` (fits for a Lambda expression too) that takes in one value and returns a boolean value. The predicate has also method `or()`.
* **Map** uses interface `Function<T, R>` and transforming collection one type into a collection of a different type.
* **ForEach** takes an argument of type `Consumer<T>`. That means that one value is accepted, but nothing is returned.
* **Reduce** takes two arguments identity and aggregator. The aggregator is the type of `BinaryOperator<T>`.
