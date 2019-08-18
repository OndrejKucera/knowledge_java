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
  * 
#### 24. Favor static member classes over nonstatic
  *
#### 25. Limit source of files to a single top-level class
  *

## 4 Generics
26-33

## 5 Enums and Annotations
34-41

## 6 Lambdas and Streams
42-48

## 7 Methods
49-56

## 8 General Programming
57-68

## 9 Exceptions
69-77

## 10 Concurrency
78-84

## 11 Serialization
85-90
