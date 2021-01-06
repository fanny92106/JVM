# Program Counter Register


## PC Register

* To keep track of what instruction is being executed
* Very small memory
* Very fast in runtime
* Every thread has its own pc register (thread-private, same life cycle with thread) to keep track of program execution
* Only area in JVM that doesn't have GC or OutOfMemoryError

