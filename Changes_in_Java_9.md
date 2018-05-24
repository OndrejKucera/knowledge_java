* **Interface private methods**
  * you can write helpers for more classes, but they won't be public
```
interface Util {
  default int getNumber() { return helper(); }
  private int helper() { return 4; }
}
```

* **Effectively final in try-with-resources**
  * use _AutoCloseable_ for a class that is used in try-catch when we leave the scope on try-catch. Then the close method is automatically called. (can be dangerous!)
```
class Resource implements AutoCloseable {
  public void foo() { ... };
  public void close() { ... };
}

public static Sample {
  Resource resource = new Resource();
  try(resource) {
    resource.method();
}
```

* **No _** 
  * underscore is not available as a name of a variable.

* **Iterate above IntStream**
  * [takeWhile](https://docs.oracle.com/javase/9/docs/api/java/util/stream/Stream.html#takeWhile-java.util.function.Predicate-)
  * [dropWhile](https://docs.oracle.com/javase/9/docs/api/java/util/stream/Stream.html#dropWhile-java.util.function.Predicate-)
```
IntStream.iterate(0, i -> i + 2)
    .takeWhile(i -> i <= 5)
    .forEach(System.out::println);
```

* **Optional**
  * Optional can be converted into the stream really easily.
  * [ifPresentOrElse](https://docs.oracle.com/javase/9/docs/api/java/util/Optional.html#ifPresentOrElse-java.util.function.Consumer-java.lang.Runnable-)
  * [or](https://docs.oracle.com/javase/9/docs/api/java/util/Optional.html#or-java.util.function.Supplier-)
```
Optional<Integer> first =
number.stream()
  .filter(e -> e > 50)
  .findFirst()
  .or(() -> Optional.of(77));
```

* **REPL**

* **Modularization**
  * the problem:
    * big jars
    * lack of clarity on dependencies
    * public is too open
    * class path -> fail late or early
    * reflection can be used when module is opened or module opens a package
  * JDK Modularized
    * module: collection of data with name, requires (only modules), exports (only packages)
    * every JDK module depends on java.base
    * public is not the same anymore
  * Create module:
    * javac ... => compile the code
    * jar ... => jar all *.class
    * jar -f *.jar -d => says what is in jar file
    * java -p [module_path] -m module/class => run the code
    * module-info.java
```
module com.name {
  requires java.base; 
  requires transitive com.for.all;
  exports com.name.best;
}
```

