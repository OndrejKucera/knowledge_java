Java Memory Management
===========================

* JVM can trace through and find all objects and arrays are still referred to, no matter how indirectly.
* Different VM implementations handle garbage collection in different ways
* Method `Thread.dumpStack()` shows methods that have their frame on the stack
### Garbage Collector
* **Parallel** - garbage collector that uses multiple threads to perform collection
* **Concurrent** - run at the same time as application threads are still running
### Memory Leaks in Java
* leak - memory is allocated and never reclaimed
* leaks in Java - if valid (but unused) reference to an unused object is left hanging around, i.e. when methods run ‘forever’, the local variables in the method can hold object references much longer than they are actually required.
* Island of Isolation - group of objects that reference each other but they are not referenced by any active object in the application.
### GC Algorithms
* JVM has data structure that keeps track of allocated and free memory (kind of linked list)
* **Reference Counting Algorithm** - one of the first algorithms, every object has a counter that shows how many references points to it. When the counter is zero then the object can be reclaimed. It can **not recognize cycles**
* **Mark and Sweep Algorithm** - iterates through allocation table and marking each object as dead. Starting from the local variables that point into the heap, follow all references. When we reach an object that we haven’t seen yet, we will mark it as alive. Sweep all that is marked as dead. It has **stop-the-world pause** problem and fragmented data. (CMS - Concurrent Mark and Sweep)
* **Stop and Copy Algorithm** the heap is split into two parts. When the memory is full live objects are copied from one part to another.
* **Generation algorithms** - Move long live object into different memory space. Objects are created in Eden and removed by non-deterministic GC. GC cycle runs when necessary. **Heap is divided** into two generations **young** (Eden, two survivor spaces) **and old**. An object is promoted into old generation after survived few GC cycles.
* **G1** - (since Java 7) The Garbage-First collector is a server-style garbage collector, targeted for multi-processor machines with large memories. G1 is a replacement for CMS. The heap is divided into regions (1MB - 32MB).  It solves the problem with fragmentation. The flag `–XX:+UseG1GC` 
  * String deduplication - G1 collector identifies strings which are duplicated across a heap and correct them to point into the same internal char[] array. Flag: `-XX:+UseStringDeduplicationJVM`
  * https://www.infoq.com/articles/G1-One-Garbage-Collector-To-Rule-Them-All
  * http://www.oracle.com/technetwork/tutorials/tutorials-1876574.html
  * http://www.journaldev.com/2856/java-jvm-memory-model-memory-management-in-java
  * http://product.hubspot.com/blog/g1gc-fundamentals-lessons-from-taming-garbage-collection
