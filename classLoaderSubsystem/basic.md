#  Class Loader Systems



## Function


* to load .class file from local disk or web into memory




## Internal Structure


￼![jvmByteCodeImg](./imageDir/jvmByteCodeImg.png)




## Process


￼![jvmByteCodeImg](./imageDir/classLoadProcess.png)


### Loading

* get binary stream of .class from class name
* transfer static storage of class stream into runtime data structure in method area
* generate an instance of java.lang.class of this class, as interface to be accessed


### Loading Source
* local disk (local file system)
* web 
* zip
* ...



