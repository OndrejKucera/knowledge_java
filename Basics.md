Basics
===============

## Methods
* Method modifiers: abstract, final, native, public, protected, private, static, strictfp, synchronized
* `abstract` when method is abstract then the class has to be as well
* `final` method can not be overridden or hidden. All private method are final
* `native` implementation is some platform-dependent (i.e. written in C). method has no body
* `static` method is associated with class itself rather than with instance of class
* `strictfp` method strictly uses floating-point arithmetic even when it could be less accurate
* `synchronized` thread-safe method. Before invoking synchronized method a lock for method (static class) or instance (non-static method) has to be obtained
* `default` can be used only in interfaces. It says that there is provide default implementation (since Java 8)
Method signature can contain checked exception
* `...` variable-length argument lists. It can be used in parameter of method e.g. (int...  rest), the last argument can be repeated, the rest is declared as array
* **Virtual method**: Interpreter checks the actual runtime type of the object referred to by the variable and then finds the method that is appropriate for that type.
* **Overriding** (method) is not hiding (for static methods, fields). Hidden code is still possible to access.
* **Overloading** (method) means that there are more methods with the same name, but they have different parameters.

## Reference Types
* **5 types**: [class](../master/Basics.md/#classes), [interface](../master/Basics.md/#interfaces), [enumerate](../master/Basics.md/#enums), [annotation](../master/Basics.md/#annotations), [array](../master/Basics.md/#arrays)
* They are user-defined, can be "unlimited" number of them
* Memory for reference types (objects) is **dynamically allocated on [HEAP](../master/Java_Virtual_Machine.md#jvm-memory)**
* When object is passed to method, only reference to memory is passed (the memory is NOT copied) => Java is strictly **pass-by-value** -> it sends copy of reference
* Java program can not manipulate (like C) with references
* Can be **converted** - widening conversions (allowed automatically by the compiler) or narrowing conversions that require a cast (and possibly a runtime check).

### Classes
* A class is a named collection of fields that hold data values and methods.
* Operator `new` creates new object (an instance of a class). There are two other ways. Instance can be created by dynamic loading mechanism or deserializing
* Instance of a class represents a Java data type and contains metadata `Class<?> typeIntArray = int[].class`
* `abstract` it's incomplete and can't be instantiated. When a class has at least one abstract method then it has to be abstract. But abstract class doesn't have to have any abstract method.
* `final` class can't be extended 
* If the field is static and final it's compile-time constant
* `public static` field is essentially a global variable!!! (don't use it without final)
* `transient` specifies that a field is not part of the persistent state of an object and it doesn’t need to be serialized with the rest of the object
* `volatile` semantic for concurrent use. The field must be read from and flushed to main memory (not cached).
* `strictfp` all its methods behave as if they were declared strictfp
* Every object has superclass `java.lang.Object`
* Class has also static constructor `static { }`
* Signature of class can also declare one or more interfaces
 
### Arrays
* Type of object which holds zero or more primitive values or references
* Instance of array is object same as instance of class
* **Memory usage**: Array has object **header 12 bytes** (to accommodate a four-byte array length), the memory usage for stored object **reference is 4 bytes**  (primitive types are different). If the total memory usage of the array is not a multiple of 8 bytes, then the **size is rounded up** to the next multiple of 8 (just as for any other object).
* Implements `Cloneable` (array can always be cloned), `Serializable` (any array can be serialized if its element type can be too)
* When array is created then every element is automatically initialized to default value 
* Maximum length of an array is `Integer.MAX_VALUE` (means NO long)
* Method `clone()` makes shallow copy of array (means only references are copied not objects)
* Good to use method `System.arraycopy()` for make **deep copy** of array
* Arrays can be converted to an another type of array
* `java.util.Arrays` has lot of utility methods as sorting, searching, comparing 
 
### Interfaces
* All mandatory methods are implicitly `abstract` and `public`
* Interface doesn’t define any instance fields. Fields are an implementation detail and interface is specification not implementation
* May contain nested types and it is implicitly public and static
* There is allowed (since Java 8) `default` method that is important for backward compatibility and `static` (flaw in the design) method, which can not be overridden
* Not possible to make an instance of an interface (there is no constructor) 
* Interface can extend other interfaces 
* Class has to declare all method of all interfaces, which implements, otherwise it has to be abstract
* **Marker interface**: empty interface, a technique to provide additional information about an object. By method instanceof() can be checked. (i.e. java.io.Serializable)
 
### Enums
* It have limited functionality, all (implicitly) extend `java.lang.Enum`
* All enums are effectively `static`, if it is member of class
* It **can not be extended**, therefore enums themselves are always `final`
* It may implement interface
* You can use `Enum` for **singleton pattern**. It will automatically support serialization and also guarantee thread-safety. Plus, it already has the private constructor.
 
### Annotations
* Specialized kind of interface that annotates some part of code
* Annotations **do not change the action** of a compiled program but can change how a program is **treated by a compiler** (useful hint to compiler and IDE)
* It should not change semantic of the program and instead provide only information for compiler etc.
* There are **3 types** of annotations: marker, single value and full  
#### Java defines built-in annotations
* There are many imported from `java.lang.annotation`: `@Target`, `@Retention`, atd.
* 5 are included in `java.lang`: `@Deprecated`, `@Override` and `@SuppressWarnings`, `@SafeVarargs`, `@FunctionalInterface`
* `@FunctionalInterface` (interface can be used as a target for lambda expression)
* All annotations extend `java.lang.annotation.Annotation` interface
* **meta-annotations** for specifying where new annotation type should be used. Two type: `@Target` and `@Retention`

## Generic types
* <T> it's called _type parameter_
* It is not possible to use primitive types as value for _type parameter_
* **Diamond syntax** is use from Java 7, less verbosity
* Generic types are visible **only at compile time**. It is stripped out by _javac_ and is not reflected in the bytecode (it can make some code illegal i.e. overload methods)
* **Wildcards** `<?>` is concept of unknown type
* **Bounded wildcards** `<? extends List>`
* Generic method: is able to take instance of any reference type `public static <T> T comma(T a, T b)`

## Nested Types
* Are used for two reasons: code needs especially **intimate access** (bend rules of encapsulation), required for a specific reason in a very small **section of code**.
### 4 types
* Static member types: works like regular top-level (nested interface, enum and annotation are implicitly static), it can access static members of the class
* Nonstatic member classes: is simply member type, has access to all fields and methods, only class can be nonstatic member types, is always associated with the instance of the enclosing type
* local classes:  has its own copy of local variables, Java implements ‘closures’ as local classes, anonymous classes (has no name), and lambda expressions (that replaces anonymous classes)
 
## Packages
* Package is a named collection of (related) classes
* `java.lang`: contains most fundamental classes of language
* `java.util`: contains utility classes
* `java.io`: contains classes for input and output
* `java.net`: classes for networking
* **CLASS PATH** - let know interpreter where to look for other classes
* Command `java` run interpreter, jar archive '-jar' or '-classpath' can be used
 
## java.lang.Object
* `toString()` returns textual representation of an object
* `equals()`, `hashCode()` if two objects are equal they should have same hashes. When method equals() is overridden then method hashCode() must be overridden too
* `Comparable::compareTo()`: for ordering
* `clone()` works only if `java.lang.Clonable` interface is implemented. Use rather copy by constructor!
* `finalize()` is called by the garbage collector on an object when garbage collection determines that there are no more references to the object
* `getClass()` returns the runtime class of this object
* `notify()` wakes up a single thread that is waiting on this object's monitor
* `wait()` causes the current thread to wait until another thread invokes the notify()
 
## Exceptions
* There are 2 types of exceptions - checked and unchecked
* **Checked exceptions** arise under well-defined circumstances. Application may be able to partially or fully **recover**
* The [JVM](https://github.com/OndrejKucera/java_knowledge/wiki/Java-Virtual-Machine) doesn’t know any such thing as checked exception, only the Java language does.
* Use **unchecked exception** when there is **no recovery**. For example, when the memory of the server is overused. Examples of unchecked exceptions are OutOfMemoryError or NullPointerException
* Subclass of Exception is RuntimeException is also unchecked
* It is an object of `java.lang.Throwable`, which has one of two subclasses `java.lang.Error` and `java.lang.Exception`
* It is not good practice catch `Exception` object that is an `Error`. They are errors from the [JVM](https://github.com/OndrejKucera/java_knowledge/wiki/Java-Virtual-Machine) and are the most serious kind of Exception in Java.
* Method `getMessage()` human readable text, which specified problem
* `Exception` has four public constructors: custom exceptions classes should implement all of them.
* Don't lose a Stacktrace - use `throw new MyException(exception)`
* Don't forget to close the resources - the `finally` block 

## Javadoc
* `@author` name
* `@version` text
* `@param` parameter-name description
* `@return` description
* `@exception` full-classname description (@throws full-classname description)
* `@depricated` explanation
* `@see` reference
* `{@link reference}`
* **reference**: `java.io.InputStream#reset`
