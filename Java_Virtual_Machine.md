Java Virtual Machine
========================

* Abstract computing machine (i.e. JVM HotSpot)
* JVM parameters:
  * `-Xms<heap size>[g|m|k] -Xmx<heap size>[g|m|k]`
  * `-XX:MaxMetaspaceSize=<metaspace size>[g|m|k]`
  * `-Xmn<young size>[g|m|k]`
  * `-XX:SurvivorRatio=<ratio>`
  * `-XX:+HeapDumpOnOutOfMemoryError`
  * ...
* **Class Files**
  * It has very specific layout with section of magic number, standard version, constant pool, access flag (public, ...), class name, inheritance info, implemented interfaces, fields, methods, attributes
  * The often used section is the constant pool. It holds representation of all methods, classes, fields, and constants that class needs to refer to
* **Class Object**
  * Class object can be obtained by method `o.getClass()`, `String.class`, `Integer.TYPE`. Class object contains metadata - **methods**, **fields**, **constructors**
* **Memory Addresses**
  * JVM memory is an **array of bytes** with addresses (pointer), where one field has 4 bytes.
  * **Java references** are called _handles_. It is a pointer to a pointer. Second pointers are stored in the special table.
* **Memory Object**
  * http://www.slideshare.net/cnbailey/memory-efficient-java
### Class Loader
**Add new types to running JVM** process and it is only way how new code can enter a system.
  * **loading** - loader reads Class Files and generates binary data into method area. For every class is stored - type, name and parent name, constants, references (class, field, method), method code. After loading class object, the JVM creates (only one) object of type Class in the Metaspace (non-heap memory).
  * **linking**
    * verification - loader verify the correctness of file `.class` and bytecode for a preventing the JVM from undefined state or crash. JVM allocates memory for class variables. 
    * preparations and resolution - check whether all classes that are necessary are known to the runtime if not new loading process can be started. (Optionally) Replacing symbolic references from the type with direct references.
  * **initializing** - all static variables are assigned with their values defined in the code and static blocks (if any) are run.
### Classloader Hierarchy
The loader try to resolve and load class only if parent is unable 
* Primordial classloader - first class loader in any JVM process. It is used to load core system classes
* Extension classloader - used only load JDK extension 
* Application classloader - loads application code from classpath
* It is possible to define your own loader (then you will need reflection)
### JVM Memory
http://blog.jamesdbloom.com/JVMInternals.html#stack_restrictions 
https://dzone.com/refcardz/java-performance-optimization 
* **Heap** - contiguous (shared) block of memory, which is reserved at JVM startup. It is used for all new objects. (4 parts: eden, 2 survivor space, old generation)
  * OutOfMemoryError - When Java Heap is full. We can use ‘Java Heap dump’ which is a snapshot of Java Heap Memory (commands jmap, jhat)
* **MetaSpace** - It is in native memory (OS heap), Metaspace auto increases its size by default, it is garbage collected when reaching `MaxMetaspaceSize`. It contains **Method area** + **code cache** (JIT optimization)
  * problem with class loader leak - There can be too many classes loaded
  * Method area - all class level information - class name, parent name class name, methods bytecode, and variables information etc. are stored, including static variables
* **Stack** - Each thread has run-time stack where frames are stored with method calls (depth 20,000-ish calls). All **local variables** of that method are stored **in their corresponding frame**
* **PC Registers** - store address of current execution instruction. Each thread has separate
* **Native Method Stacks** - a separate native stack is created for every thread. It stores native method information.
### Execution Engine
* It executes bytecode (.class), contain two **executing modes** client and server
* **Interpreter** - interprets bytecode line by line, if method is called many time, every time interpreted is required
* **Just-In-Time Compiler(JIT)** - increase the efficiency of Interpreter. It compiles entire bytecode change it to native code, whenever Interpreter see repeated method is called
* **Garbage Collector** - destroy unreferenced object from Heap Memory
### Java Native Interface (JNI)
### Native Method Libraries
