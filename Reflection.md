Reflection
=================

* Ability to examine operating and modify objects at runtime
* Working even when type and methods name are not known at compile time
* Instance can be created **reflexively** by `Class::newInstance()`
* Class object contains Method object for every method 
* **When to use reflection**
  * Good to use for flexibility and code that is unknown until runtime. Use it for accessing objects where virtually no information is known in your own code.
* **How to use reflection**
  * First step is to get to Class object and then you can get instance  
  * i.e.: reflective invocation method - `method.invoke(rcrv, args)`
* **Problems with reflection**
  * Heavy use `Object[]` to represent call arguments and Class[] when you need to specify types
  * Problematic representing of primitive types - automatic box
  * void and void.class can be problem
  * work with non-public method - the access control has to be overridden
* **Dynamic Proxies** - `java.lang.reflect.Proxies` is used for testing (mocking). Another use case can be to provide a partial implementation of an interface.
* **Method Handle**
  * Better and safer than reflection
  * `java.lang.invoke.MethodHandle`
  * One difference from reflection is access control (no setAccessible() hack)
  * MethodType: represents return type and argument types
  * Method lookup: `MethodHandles.lookup()` give us context of execution mode. It has several method `findVirtual()`, `findStatic()`, `findConstructor()`
