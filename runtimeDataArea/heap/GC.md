# Garbage Collection


## Category

* Minor GC (Young GC) : 只收集新生代 (Eden, S0, S1)  的垃圾，属于部分收集
* Major GC (Old GC) : 只收集老年代的垃圾，属于部分收集
* Mixed GC : 收集整个新生代以及部分老年代的垃圾收集
* Full GC ：收集整个java堆和方法区！！！的垃圾，属于整堆回收



## Triger GC 机制

### Minor GC

* 当Young Gen内存不足时，就会触发Minor GC, 这里的Young Gen 指的是Eden代满，Survivor满不会引发GC (每次 Minor GC会清理年轻代的内存)
* 因为Java的对象都具备朝生夕灭的特性，所以Minor GC非常频繁，一般回收速度也比较快
* Minor GC会引发 STW (stop the world), 暂停其他用户的线程，等垃圾回收结束，用户线程才恢复运行


### Major GC

* 发生在老年代的GC，经常会伴随至少一次的Minor GC (非绝对)
* Major GC的速度一般会比Minor GC慢10倍以上，STW的时间更长
* Major GC后内存还不足就报OOM了，OutOfMemoryError


### Full GC

* 触发Full GC的情况：1) 调用System.gc() 时， 系统建议执行Full GC， 但是不必然执行
    2) Old Gen空间不足
    3) 方法区空间不足
* Full GC是开发或调优中尽量要避免的，这样STW的时间会短一些
