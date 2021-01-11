# JVM Stack


* 每个线程在创建时都会创建一个虚拟机栈，其内部保存一个个的栈帧 (stack frame), 对应着一次次的Java方法调用
* 是线程私有的, 是线程私有的，生命周期与线程一致
* 主管Java程序的运行，保存方法的局部变量 (8种基本数据类型, 对象的引用地址), 部分结果, 并参与方法的调用和返回


## Advantage

* 快速有效的存储方式，访问速度仅次于程序计数器
* 对于栈来说，不存在垃圾回收问题 NO GC



## 可能出现的异常

* JVM 允许Javad栈的大小是动态的或者是固定不变的
* 如果采用固定大小的JVM，则每个线程的Java虚拟机栈容量可以在线程创建的时候独立选定。如果线程请求分配的栈容量超过JMV允许的最大容量，JVM会抛出一个StackOverflowError异常
* 如果JVM栈是可以动态扩展，并且在尝试扩展的时候无法申请到足够的内存，或者在创建新的线程时没有足够的内存去创建对应的虚拟机栈，那JVM将抛出一个OutOfMemoryError异常



## 栈帧 (stack frame) 的内部结构

* 局部变量表 (local variables)
* 操作数栈 (operand stack)
* 动态链接 (dynamic linking)
* 方法返回地址 (return address)



## 局部变量表 (local variables)

* 最小的存储单元是槽 (slot)
* 局部变量必须在声明时显式赋值
member variable
    class variable -- get default value when loading it, get initialized during class loading initialization process
    instance variable -- get initialized in heap when class instance get initialized
local variable -- must get instantialized before using it, else compiler will complain
* 栈帧中，与JVM性能调优最为密切的就是局部变量表。局部变量表越大，栈帧越大，一个栈中可以入栈的栈帧数量越少，given一个指定的栈大小
* 局部变量表的变量也是垃圾回收(GC)的根节点，被局部变量表中直接或间接引用的对象都不会被回收
