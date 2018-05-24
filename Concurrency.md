Concurrency
=============

* **Thread** - It is smaller unit than process, each thread can be **scheduled independently** and has its **own stack** and **program counter** but **shares memory and objects** with other threads in the same process.
* Thread Lifecycle:
  * `NEW` - created, but not started yet
  * `RUNNABLE` - is running or is available to run
  * `BLOCKED` - not running, waiting to acquire lock
  * `WAITING` - not running because it has called Object.wait() or Thread.join()
  * `TIMED_WAITING` - not running because it has called Thread.sleep()
  * `TERMINATED` - execution completed
* Thread methods:
  * `getId()` - id number of thread
  * `setName()` - getName(), name of the thread can be set
  * `getState()` - returns Thread.State
  * `isAlive()` - is thread still alive?
  * `start()` - creates new application thread and schedule it
  * `interrupt()` - the interrupt status of the thread will be set to true
  * `join()` - thread waits until the thread corresponding to the Thread object has died
  * `setDeamon()` 
  * **DO NOT USE**: stop(), suspend(), resume(), and countStackFrames(), destroy()
