### Parallel Computing / Concurrency

Common questions on parallel computing / concurrency:

1. multi-process vs multi-thread
  1. Multi-threading Pros
    * easy / fast to shared data between threads (it's just shared memory with an unified address space)
    * easy to communicate with parent process
    * beneficial for large dataset. Don't have to pay the penalty of distributing/duplicating data across process boundaries.
    * supported by many 3rd party libraries (OpenMP)
  1. Multi-threading Cons
    * no isolation: one thread crash ==> whole process crash
    * multi-threaded apps are hard to debug. (race conditions, locks)
    * Too many threads ==> lots of context switching
    * No scalable path to multiple machines / public cloud
  1. Multi-process Pros
    * process crashes won't harm other processes (you can recover process crashes, think microservices)
    * much easier to debug an atomic process
    * Less locking (unless you try to share memory / resources between multiple process)
    * Scalable across machines
  1. Multi-process Cons
    * communication between processes are more complicated and are less efficient
    * smaller set of supporting libraries (and are generally not portable across different platform)
  
  TL;DR 
  * Generally if you need to maintain synchronized state then prefer threads. 
  * Do you have large dataset? Then prefer threads. 
  * Do you want easier development / debugging + finer-grain control? prefer processes
  * Do you want to be able to scale into the cloud? prefer processes

