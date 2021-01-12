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

* 用数组在实现，最小的存储单元是槽 (slot)
* 局部变量：方法参数，本地（局部）变量
* 局部变量必须在声明时显式赋值
member variable
    class variable -- get default value when loading it, get initialized during class loading initialization process
    instance variable -- get initialized in heap when class instance get initialized
local variable -- must get instantialized before using it, else compiler will complain
* 栈帧中，与JVM性能调优最为密切的就是局部变量表。局部变量表越大，栈帧越大，一个栈中可以入栈的栈帧数量越少，given一个指定的栈大小
* 局部变量表的变量也是垃圾回收(GC)的根节点，被局部变量表中直接或间接引用的对象都不会被回收



## 操作数栈 (operand stack)

* 用数组实现，主要用于保存计算过程的j中间结果，同时作为计算过程中变量临时的存储空间
* 如果被调用的方法带有返回值，其返回值会被压入当前栈帧的操作数栈中，并更新pc register下一条要执行的字节码指令
* 栈顶缓存技术 (top-of-stack cache): 为了解决频繁地对操作数栈入栈/出栈的操作，HotSpot JVM的设计者提出将栈顶元素全部缓存在物理CPU的寄存器中，以此降低对内存读/写的次数，提升执行引擎的执行效率



## 动态链接 (dynamic linking)

* Java源文件被compile到字节码文件时，所有常量，变量和方法的引用都被作为符号引用 （symbolic reference) 保存在class文件的constant pool中，便于指令识别，介绍文件size



## 虚方法 vs 非虚方法

* 非虚方法: 在编译时就确定了具体的调用版本，这个版本在运行时是不可变的(不能有runtime override), 这样的方法称为非虚方法
* 例如：static method, private method, final method, constructor method (构造器不能被继承，每个类只能有一个), parent class method
* 其他的都是虚方法



## 方法调用 (method call)

* 静态调用 (static link/ early bounding) : compile时确定具体执行的方法，这个版本在运行时是不可变的，将symbolic reference转化成direct reference； 这样的方法叫非虚方法 (non-virtual method), 与c++对应
* 动态调用 (dynamic link/ late bounding) : runtime时才能具体确定所要执行的方法，同上; 这样的方法叫 (virtual method)



## 虚拟机提供的方法调用指令

### 普通调用指令: 
* invokestatic: 调用x静态方法  -- 静态链接
* invokespecial: 调用<init>方法，私有方法，指定的父类方法  -- 静态链接
* invokevirtual: 调用所有虚方法 （除了final， 因为被final修饰了的方法属于静态链接)
* invokeinterface: 调用接口方法

### 动态调用指令: java7
* invokedynamic: 动态解析出需要调用的方法。然后执行







