# Heap




## Basic

* Main object storage area in JVM
* Heap size is set when JVM initializes, but can use -Xmx, -Xms to set heap(Young Gen + Tunure Gen) size; 最小的堆内存为可用物理内存的1/64, 最大的堆内存为可用物理内存的1/4; 工程中设置heap的初始堆内存 = 最大堆内存，以减少在GC过后系统频繁扩容/释放的压力
* The largest area in JVM
* OOM & GC  




## Generation

* Young Generation
* Eden (几乎所有Java对象都是在Eden区被new出来的)
    * Survivor0
    * Survivor1
* Tenure Generation (存放新生代中经历多次GC仍然存活的对象，或新生代中无法存放的大对象)
* 【Permaneng Genenration in jdk 7; Meta Space in jdk 8 & later -- belong to Method Area (方法区)】




## 分代思想

* 不同对象的生命周期不同，70% - 99% 的对象是临时对象
* heap部分代也是完全可以的，分代的唯一理由就是优化GC性能




## 内存分配策略 (Object Promotion Rule)

* 优先分配到Eden （70% - 99% 朝生夕死)
* 大对象直接分配到老年代 -- (内存连续的大对象, eg: String/ big array，尽量避免程序中出现过多的大对象)
* 长期存活的对象分配到老年代
* 动态对象年龄判断: 如果Survivor区中相同年龄的所有对象大小的总和大于Survivor空间的一半，年龄大于或等于该年龄的对象可以直接进入老年代, 无需等到MaxTenuringThreshold中要求的年龄
* 空间分配担保: -XX: HandlePromotionFailure




## Parameter 

可视化工具检测 jvisualvm (Library/jvm/bin/jvisualvm)
Idea 里面的 run/ edit config来配置运行参数
* -XX: +PrintFlagsInitial: 查看所有参数的默认初始值
* -XX: +PrintFlagsFinal: 查看所有参数的最终值
* -Xmx (== -XX: MaxHeapSize) [-X 代表jvm 运行参数, m 代表 memory,  x 代表 max]
* -Xms (== -XX: InitialHeapSize) to set heap size [s 代表 start]
* -Xmn: 设置新生代的大小
* XX: PrintGCDetails 显示和GC相关的内存heap中不同代使用大小
* XX: NewRatio=2 设置新生代于老年代的比例，默认值是2； 一般情况下无需修改
* XX: SurvivorRatio=8 设置新生代中Eden区和另外两个Survivor空间的占比，默认值是8：1：1
* -XX: MaxTenuringThreshold: 设置新生代垃圾的最大年龄




## GC

* 频繁在新生区收集，较少在养老区收集，几乎不在永久区/元空间收集

