[Effective Java](https://www.goodreads.com/book/show/34927404-effective-java)
===============

## Creating and Destroying Objects
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

## Methods Common to All Objects
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

## Classes and Interfaces
#### 15. Minimize the accessibility of classes and members
 - TODO:
#### 16. In public classes, use accessor methods, not public fields
 - TODO:
#### 17. Minimize mutability
 - TODO:
#### 18.
