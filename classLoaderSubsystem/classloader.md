# Class Loader

## Category
    * Bootstrap class loader
    * User customized class loader
    

### Bootstrap class loader -- load core class library
    * Implemented by C/C++, embedded in JVM
    * Load jvm core library (JAVA_HOME/jre/lib/rt.jar, resource.jar or sun.boot.class.path) to provide class needed by JVM
    * Not inherit java.lang.ClassLoader, no parent classloader
    * Load extension class loader & app class loader, as their parent class loader
    * Bootstrap class loader only load package named with java, javax, sun etc
    

### Extension class loader -- load other extension class library
    * Implemented by Java
    * Inherited from ClassLoader class
    * Parent classloader is Bootstrap class loader
    * Load class in jre/lib/ext (扩展目录), also jar created by user if put into this dir
     

### Application class loader -- 
    * Implementd by Java
    * Inherited from ClassLoader class
    * Parent classloader is Bootstrap class loader
    * Load environmental variable classpath or java.class.path
    * Default class loader, which load java app class
    
    
