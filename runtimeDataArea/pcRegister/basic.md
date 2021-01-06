# Program Counter Register


## PC Register

* To keep track of what instruction is being executed
* Very small memory
* Very fast in runtime
* Every thread has its own pc register (thread-private, same life cycle with thread) to keep track of program execution
* Only area in JVM that doesn't have GC or OutOfMemoryError


## Question: why use PC register?

* 因为CPU需要需要不停地切换各个线程，当切换回来以后，就需要知道接着从哪里开始继续执行



