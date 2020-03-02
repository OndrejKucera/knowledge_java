[Effective Java](https://www.goodreads.com/book/show/34927404-effective-java)
===============

## 1 Creating and Destroying Objects
#### 1. Consider static factory methods instead of constructors
   * (+) they have names
   * (+) not required to create a new object each time
   * (+) return object of any subtype
   * (-) classes without `public`/`protected` constructor cannot be subclassed
#### 2. Consider a builder when faced with many constructor parameters
   * (+) easier to read than telescoping constructor
   * (+) object cannot be in an inconsistent state -> immutability
   * (+) [Builder pattern](https://github.com/OndrejKucera/knowledge_scala_design_patterns/blob/master/Builder.md) simulates optional parameters
#### 3. Enforce the singleton property with a private constructor or an enum type
   * (-) difficult to test its clients
   * (+) private constructor: `final` field + `static` method;
   * (-) `enum` type: provides serialization and prone to a reflection attack
#### 4. Enforce noninstantiability with a private constructor
   * (+) for a class that is just a grouping of `static` methods and fields
#### 5. Prefer dependency injection to hardwiring resources
   * (+) pass resource into the constructor when creating a new instance
#### 6. Avoid creating unnecessary objects
   * (-) don't do this: `new Integer(5)`, `new String("text")`
   * (-) you can avoid creating unnecessary objects by using a static factory method
   * (-) prefer primitives and watch out for unintentional autoboxing
#### 7. Eliminate obsolete object references
   * (-) nulling out object reference should be the exception rather than the norm
   * (-) one of the sources of memory leaks is caches.
   * (-) or listeners and callbacks
#### 8. Avoid finalizers and cleaners
   * (-) finalizers are unpredictible, often dangerous, unnecesarry
   * (+) object must track whether it has been closed. Your class should implement `AutoCloseable`. 
#### 9. Prefer try-with-resources to try-finally

## 2 Methods Common to All Objects
#### 10. Obey the general contract when overriding equals
   * reflexive `(x.equals(x) == true)`, symmetric `(x.equals(y) == y.equals(x))`, transitivite `(x=y, y=z, x=z)`, consistent, non-nullity (`x.equals(null)` must return `false`)
   * it can not depends on unreliable resources
   * use `==` to checkif the argument is a reference to this object
   * use `instanceof` whether the argument has correct type (cast argument to cerrect type)
   * override the hashcode too
#### 11. Always override hashCode when you override equals
   * you must override `hashCode` method in every class that overrides equals
   * `hashCode` have to consistenly returns same value (during execution of application)
   * if `x.equal(y) == false` then `x.hashCode() == y.hashCode()` but if the `x.equal(y) == false` it doesn't mean that `x.hashCode() != y.hashCode()`
   * hash function should distribute any reasonable collection of unequal instances uniformly across all int values
   * `result = 31 * result + c`
   * consider caching hash result?
#### 12. Always override toString
   * providing a good `toString` implementation makes your class much more pleasant to use
#### 13. Override clone judiciously
   * In practice the class implementing `Clonable` is expected to provide a properly functioning public clone methond.
   * Better approach to object copying is to provide a copy constructor ( `public Yum(Yum yum)` ) or copy factory ( `public static Yum newInstance(Yum yum)` )
#### 14. Consider implementing Comparable
   * Use of the relation operators `<` and `>` in `compareTo` methods is verbose and error-prone and no longer recommended. Instead use static compare methods in boxed primitive classes or the comparator construction methods in `Comparator` `construction.

## 3 Classes and Interfaces
#### 15. Minimize the accessibility of classes and members
   * make each class or member as inaccesible as possible
   * instance of fields of public classes should rarely be public
   * classes with public mutable fields are not generaly thread-safe
   * it is wrong for class to have `public static final` array field, or accessor that returns such a field. -> client is able to modify content.
#### 16. In public classes, use accessor methods, not public fields
   * if a class is accessible outside its package, provide accessor methods
   * if class is package-private or is private nested class, there is nothing inherently wrong with exposing its data fields.
#### 17. Minimize mutability
   * immutable object are simple
   * immutable objects are inherently thread-safe; they require no synchronization
   * immutable objects can be shared freely
   * immutable objects make great building blocks for other objects
   * Constructors should create fully initialized objects with all of their invariats estabilished
   * to make class immutable:
     * don't provide the methods that modify the object's state
     * ensure that the class can't be extended
     * make all fields final
     * make all fields private
     * endsure exclusive access to any mutable components
   * (-) the major disadvantage of immutable class is that they require a seperate objects for each distinct value
#### 18. Favor composition over inheritance
  * (-) Inheritance of ordinary class can be dangerous
    * inheritance violate encapsulation and leeds to fragile software
  * Inheritance is appropriate in case when subclass is really type of superclass.
  * It is safe use inheritance inside the package because superclass and subclass is under control. It is also safe extend classes which are documented and created for the purpose
  * (+) It is possible to avoid inherince by composition. Into your new class, create private field of reference to existed class. Your new class will be wrapper. 
#### 19. Design and document for inheritance or else prohibit it
  * The class has to document its use of overridable methods. You can use Implementation Requirements
  * The only way to test a class design for inheritance is to write subclasses. -> test the class by subclass is must!
  * Constructors must not call overridable methods.
  * Designing a class for inheritance requires is great effort and place limitation on the class.
  * One of the solution - prohibit inheritance of classes that are not design to be safely subclassed
    * use `final class`
    * or or make all constructors private
#### 20. Prefer interfaces to abstract classes
  * Existing classes can easily implement new interfaces. It is not easy to do with classes - Java permits only single inheritance. You have to hierarchically extends the class. 
  * Interfaces allow for the construction of nonhierarchical type frameworks.
  * Interfaces are ideal for defining mixins. 
  * Interfaces enable safe, powerful functionality enhancements via the wrap- per class idiom
#### 21. Design Interafaces for prosperity 
  * It is not always possible to write default methods for all implemation cases.
  * Although, it is possible to add default methods into existing interfaces, there is great risk in doing so. 
  * It is critical to test all new interface which you want to release.
#### 22. Use interafaces only to definne types 
  * Don't define constants in interfaces - it is poor use of interface. Constant is implemation detail.
  * Use public static final in class
#### 23. Prefer class hierarchies to tagged classes
  * Tagged clacc represent more "flavours" in one class, for example, by private field with enum. 
  * Tagged classes are verbose, error-prone, and inefficient
  * Create abstract class with abstract method instead.
#### 24. Favor static member classes over nonstatic
  * Make a static rather than a nonstatic member class
    * without `static` each instance will have hiddent reference to its enclosing instance
    * storing this reference takes time and space
    * enclosing instance can be retained when it would otherwise be eligible for garbage collection
#### 25. Limit source of files to a single top-level class
  * Never put multiple top-level classes or interfaces in a single source file. Following this rule guarantees that you can’t have multiple definitions for a single class at compile time. 

## 4 Generics
#### 26. Don’t use raw types
  * If you use raw typesc (i.e. List), you lose all the safety and expressiveness benefits of generics. They are in language because of compatibility.
  * You lose type safety if you use a raw type such as `List`, but not if you use a param- eterized type such as `List<Object>`
  * You must use raw types in class literals. `List.class` is ligal,  `List<String>` is not legal
#### 27. Eliminate unchecked warnings
  * Eliminate every unchecked warning that you can
  * If you can’t eliminate a warning, but you can prove that the code that provoked the warning is typesafe, then (and only then) suppress the warning with an `@SuppressWarnings("unchecked")` annotation.
  * Always use the SuppressWarnings annotation on the smallest scope possible
  * Every time you use a `@SuppressWarnings("unchecked")` annotation, add a comment saying why it is safe to do so.
#### 28. Prefer lists to arrays
  * Arrays and generics have very different type rules.
  * Arrays are covariant and reified; generics are invariant and erased. As a consequence, arrays provide runtime type safety but not compile-time type safety, and vice versa for generics.
#### 29. Favor generic types
  * Generic types are safer and easier to use than types that require casts in client code.
  * When you design new types, make sure that they can be used without such casts. This will often mean making the types generic.
  * If you have any existing types that should be generic but aren’t, generify them. This will make life easier for new users of these types without breaking existing clients.
#### 30. Favor generic methods
  * Just as classes can be generic, so can methods
  * The type parameter list, which declares the type parameters, goes between a method’s modifiers and its return type. `public static <E> Set<E> union(Set<E> s1, Set<E> s2)`
  * Generic methods, like generic types, are safer and easier to use than methods requiring their clients to put explicit casts on input parameters and return values.
#### 31. Use bounded wildcards to increase API flexibility
  * User wildcard types on input parameters that represent producers (extend) or consumers (super)
  * Do not user bounded wildcard as return type
  * If the user of a class has to think about wildcard types, there is probably something wrong with API
  * Use Comparable<? super T> in preference to Comparable<T>
  * If a type parameter appears only once in a method declaration, replace it with a wildcard
#### 32. Combine generics and varargs judiciously
  * varargs and generics do not interact well 
  * Use @SafeVarargs on every method with a varargs parameter of a generic or parameterized type,
#### 33. Consider type safe heterogeneous containers

## 5 Enums and Annotations
#### 34. Use enums instead of int constants
  * Use enums any time you need a set of constants whose members are known at compile time.
  * It is not necessary that the set of constants in an enum type stay fixed for all time.
#### 35. Use instance fields instead of ordinals
  * Never derive a value associated with an enum from its ordinal; store it in an instance field instead
#### 36. Use EnumSet instead of bit fields
#### 37. Use EnumMap instead of ordinal indexing
#### 38. Emulate extensible enums with interfaces
  * while you cannot write an extensible enum type, you can emulate it by writing an interface to accompany a basic enum type that implements the interface.
#### 39. Prefer annotations to naming patterns
  * There is simply no reason to use naming patterns when you can use annotations instead
#### 40. Consistently use the Override annotation
  * 
#### 41. Use marker interfaces to define types
  * Marker interfaces define a type that is implemented by instances of the marked class; marker annotations do not.
  * Another advantage of marker interfaces over marker annotations is that they can be targeted more precisely.
  * The chief advantage of marker annotations over marker interfaces is that they are part of the larger annotation facility.

## 6 Lambdas and Streams
#### 42. Prefer lambdas to anonymous classes
  * lambdas lack names and documentation; if a computation isn’t self-explanatory, or exceeds a few lines, don’t put it in a lambda.
  * you should rarely, if ever, serialize a lambda
#### 43. Prefer method references to lambdas
  * Where method references are shorter and clearer, use them; where they aren’t, stick with lambdas.
#### 44. Favor the use of standard functional interfaces
  * If one of the standard functional interfaces does the job, you should generally use it in preference to a purpose-built functional interface.
#### 45. Use streams judiciously
  * Using helper methods is even more important for readability in stream pipelines than in iterative code
  * You can not return from the enclosing method or throw any checked exception that this method is declared to throw.
#### 46. Prefer side-effect-free functions in streams
#### 47. Prefer Collection to Stream as a return type
  * Collection or an appropriate subtype is generally the best return type for a public, sequence- returning method.
#### 48. Use caution when making streams parallel
  * performance gains from parallelism are best on streams over ArrayList, HashMap, HashSet, and ConcurrentHashMap instances; arrays; int ranges; and long ranges
  * Not only can parallelizing a stream lead to poor performance, including liveness failures; it can lead to incorrect results and unpredictable behavior
  * Under the right circumstances, it is possible to achieve near-linear speedup in the number of processor cores simply by add- ing a parallel call to a stream pipeline
  
## 7 Methods
#### 49. Check parameters for validity
  * For public and protected methods, use the Javadoc @throws tag to document the exception that will be thrown.
  * Typically, the resulting exception will be IllegalArgumentException, IndexOutOfBoundsException, or NullPointerException
  * You can use `Objects.requireNonNull()`
#### 50. Make defensive copies when needed
  *
#### 51. Design method signatures carefully
  *
#### 52. Use overloading judiciously
  *
#### 53. Use varargs judiciously
  *
#### 54. Return empty collections or arrays, not nulls
  *
#### 55. Return optionals judiciously
  *
#### 56. Write doc comments for all exposed API elements
  *

## 8 General Programming
57-68

## 9 Exceptions
69-77

## 10 Concurrency
78-84

## 11 Serialization
85-90
