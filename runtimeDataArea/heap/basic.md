# Heap


### Basic
* Main object storage area in JVM
* Heap size is set when JVM initializes, but can use -Xmx, -Xms to set heap(Young Gen + Tunure Gen) size; 最小的堆内存为可用物理内存的1/64, 最大的堆内存为可用物理内存的1/4; 工程中设置heap的初始堆内存 = 最大堆内存，以减少在GC过后系统频繁扩容/释放的压力
* The largest area in JVM
* OOM & GC  




## Structure
* Young Generation
    * Eden (几乎所有Java对象都是在Eden区被new出来的)
    * Survivor0
    * Survivor1
* Tenure Generation
(
* Permaneng Genenration in jdk 7
* Meta Space in jdk 8 & later -- belong to Method Area (方法区)
)




## Parameter 

可视化工具检测 jvisualvm (Library/jvm/bin/jvisualvm)
Idea 里面的 run/ edit config来配置运行参数

* -Xmx (== -XX: MaxHeapSize) [-X 代表jvm 运行参数, m 代表 memory,  x 代表 max]
* -Xms (== -XX: InitialHeapSize) to set heap size [s 代表 start]
* XX: PrintGCDetails 显示和GC相关的内存heap中不同代使用大小
* XX: NewRatio=2 设置新生代于老年代的比例，默认值是2； 一般情况下无需修改
* XX: SurvivorRatio=8 设置新生代中Eden区和另外两个Survivor空间的占比，默认值是8：1：1




## GC

* 频繁在新生区收集，较少在养老区收集，几乎不在永久区/元空间收集

