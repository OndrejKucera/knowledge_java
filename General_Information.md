Generela Information
====================

## General Information
* 1996 Java 1.0
* Java is governed by Java Language Specification  (JLS)
* Class based and object oriented language
* **Statically typed**: variables have definite types. The compile-time error can occur when a value of an incompatible type is assigned to a variable. (but Java is not perfectly type-safe -> it is possible to cast)
* **Interpreted languages**: [bytecode](https://en.wikipedia.org/wiki/Java_bytecode) + [interpreter](https://en.wikipedia.org/wiki/Interpreter_(computing)) => run
* **Main properties**: portable (class files), automatic memory management ([garbage collection](../blob/master/Java_Memory_Management.md#garbage-collector)), can not directly address memory, pass-by-value, not full multiple inheritances, no operators overloading, [generic classes](https://github.com/OndrejKucera/java_knowledge/wiki/Basics#generic-types), [multithreaded](https://github.com/OndrejKucera/java_knowledge/wiki/Concurrency#concurrency), ...  
* Java **source code** is class file with extension .class. It has to be converted to Java bytecode for [JVM](https://github.com/OndrejKucera/java_knowledge/wiki/Java-Virtual-Machine#java-virtual-machine) 
class file. It is the smallest unit of functionality the platform will deal with
* **javac**: produce bytecode, But! it is not a real compiler
* Start an application: `java <arguments> <program name>`
* **bytecode**: It is an intermediate representation (half-source-half-machine code). One instruction has single byte. It means there are only 256 instructions. Why does bytecode exist? We want something efficient to run on JVM. ([big-endian](https://en.wikipedia.org/wiki/Endianness#Big))
* **JVM**: interpreter, memory management, provide cross-platform environment (and secure), self-management (optimization) 
* **[JIT](https://github.com/OndrejKucera/java_knowledge/wiki/Java-Virtual-Machine#execution-engine)**: just-in-time compilation, JVM defines the most usable part of the code and focusing optimization on it.
* **Java 8**: lambda expression, overhaul of core collection, 'default' in interfaces, ...
* **Java 9**: September 21st

## Syntax
* Document begins with a package and some import is followed
* Java is written in Unicode
* Case-sensitive and ignore whitespace
* Comments are ignored by javac
* Reserved words `const` and `goto` aren't used
* Literals: integer, float-point number, string, true, false, null
* **Primitive types**: boolean(8b, depends on JVM), char(16b), byte(8b), short(16b), int(32b), long(64b), float(32b), double(64b)
* **Integer arithmetic** in Java never produces an **overflow** or an **underflow** when you exceed the range of a given integer type. Instead, numbers just wrap around. Neither Java compiler or interpreter won’t warn you.
* float point values are represented by [IEEE 754-1985 standard](https://en.wikipedia.org/wiki/IEEE_754-1985)
* Java has **positive** and **negative zero** (depending on the direction from which the underflow occurred, and are equal), NaN for illegal operations (floating-point arithmetic never throw exceptions)
* `instanceof` is good to used for check the type before casting
* `final` is used before variable/field declaration. It means that value can not be changed after initialization
* `static final` before field means that it is compile-time constant
* **unboxing** and **auto-boxing** conversion for example from Boolean is automatically taken primitive boolean value 
* `switch` works only with int, char, byte, short, String or enum
* `synchronized` support for multithreading, it can lock some object for block of code or can be used as method modifier (then it lock class or object)
* `finally` is part of try-catch, e.g. close files and shut down network connections
* `try-with-resources` (TWR) new form of try with parameters (since Java 7)
* `assert` designs to provide assumptions in Java code, but only when it is turn on!

## Naming
* **Class**: use names that are nouns because it is designed to represent object
* **Interface**: use an adjective because it provides additional information (Annotations also). If it will be using more like an abstract super class use noun as a name.
* **Method**: the first word should be verb

## Java Command lines tools
* javac - Java source code compiler
* java - the executable that starts JVM
* jar - utility for manipulating with Java Archive (.jar)
* javadoc: produce Java documentation from Java source files
* jdes: tool for analyzing dependencies
* jstat: provide static information about java process
* jstack: produce a stack trace for each Java thread

## Java Useful Libraries
* Guice - support for dependency injection
* Guava - new collections, utility for string and collections, ...
* Spring -
* Slf4j - for logging 
* okHttp - http client
* Retrofit - handle http answers
* RxJava - reactive programming 
* Lombok - setters, getters, ...

