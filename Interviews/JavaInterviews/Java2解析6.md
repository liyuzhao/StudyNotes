对于有一定经验的开发者，在面试过程中多多少少都会被问及jvm相关知识，但是往往在实际开发中涉及较少，这里整理一些知识点做一期面试题库拿出来，希望对有用到朋友有一些参考。



小编水平有限，可以把常考题型列出来，但解答部分仅做参考，如果有知识点错误希望能够留言纠正，如果是有更好的参考答案，更加欢迎留言大家探讨，我会置顶，以上这些，下面是正题。



**Java语言中一个显著的特点就是引入了垃圾回收机制，这个大家都清楚，垃圾回收的概念这里也不做介绍，重点是垃圾回收是在什么时候开始？对什么东西，做了什么事情？**



GC何时开始：

所有的回收器类型都是基于分代技术来实现的，那就必须要清楚对象按其生命周期是如何划分的。

年轻代：划分为三个区域：原始区(Eden)和两个小的存活区(Survivor)，两个存活区按功能分为From和To。绝大多数的对象都在原始区分配，超过一个垃圾回收操作仍然存活的对象放到存活区。垃圾回收绝大部分发生在年轻代。

年老代：存储年轻代中经过多个回收周期仍然存活的对象，对于一些大的内存分配，也可能直接分配到永久代。

持久代：存储类、方法以及它们的描述信息，这里基本不产生垃圾回收。



有了以上这些铺垫之后开始回答GC何时开始：

Eden内存满了之后，开始Minor GC（从年轻代空间回收内存被称为 Minor GC）；升到老年代的对象所需空间大于老年代剩余空间时开始Full GC（但也可能小于剩余空间时，被HandlePromotionFailure参数强制Full GC）



对什么东西操作，即垃圾回收的对象是什么：

从root开始搜索没有可达对象，而且经过第一次标记、清理后，仍然没有复活的对象。 



做了什么东西：

主要做了清理对象，整理内存的工作。具体的引申如下



垃圾回收器的类型：

串行垃圾回收器（Serial Garbage Collector）

并行垃圾回收器（Parallel Garbage Collector）

并发标记扫描垃圾回收器（CMS Garbage Collector）

G1垃圾回收器（G1 Garbage Collector）



垃圾回收算法：

引用计数法

标记清除法

复制算法

标记压缩算法

分代算法

分区算法



以上这些，可以自己了解一下，这里列举几篇相关文章：

[JVM的内存区域划分](http://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247484719&idx=1&sn=c0f3a3d518dd89a08acad5f0ef0cdca6&chksm=ebd63a03dca1b315cf60bbdcd034ad22d5a0c1afe194d185fe0cf5b19ce15fb3e70630f3c9b9&scene=21#wechat_redirect)

[JVM知识点梳理](http://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247484237&idx=1&sn=79d99a5bc17453e5cdd3ca1f9ad97d13&chksm=ebd63c61dca1b5776136bf20f63e4654facf4e025e9ef01d94c7662a8916613fc86d345d3307&scene=21#wechat_redirect)

[JVM内存分配与回收](http://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247484011&idx=1&sn=2efb8e99d2ce18b6a8f640978c09ab16&chksm=ebd63d47dca1b4516161db13f20e8ef3cc2b3c055fbb06ca81e92fa5cf96215304a3067ce5c7&scene=21#wechat_redirect)

[JVM内存管理机制](http://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247484008&idx=1&sn=64340424e740f49329e9ed0ea58c03f6&chksm=ebd63d44dca1b452a491c76d088305fcb4b9ab50c29596dc3bb7941139cd6b31057a5f21900e&scene=21#wechat_redirect)

[Java虚拟机学习 - 垃圾收集器](http://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247484144&idx=1&sn=5b579333a2503296e9a3d0dcbe4b19fc&chksm=ebd63ddcdca1b4ca95dbf66b9a4de5c44fe3cf362678b89890feaf53122b55403f5c5deb7490&scene=21#wechat_redirect)





**类在虚拟机中的加载过程**



**加载Loading：**

通过一个类的全限定名来获取一个二进制字节流、将这个字节流所代表的静态存储结构转化为方法区的运行时数据结构、在内存中生成一个代表这个类的java.lang.Class对象，作为方法区这个类的各种数据的访问入口。



**验证Verification：**

确保Class文件的字节流中包含的信息符合当前虚拟机的要求，并不会危害虚拟机的自身安全。



**准备Preparation：**

正式为类变量分配内存并设置类变量初始值。



**解析Resolution：**

虚拟机将常量池内的符号引用替换为直接引用的过程。



**初始化Initialization：**

类加载过程的最后一步，到了这个阶段才真正开始执行类中定义的Java程序代码。



**使用Using：**

根据你写的程序代码定义的行为执行。



**卸载Unloading：**

GC负责卸载，这部分一般不用讨论。



以上这些抛砖引玉，欢迎留言更清晰的类加载过程，相关文章可以阅读：

[类加载器详解](http://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247484617&idx=1&sn=4cbfe7fb7e3e15bb043caf2284f5223a&chksm=ebd63be5dca1b2f395e70b081888cb62e11d75cd01ad025e9a26ebe2d2163048d8e533853785&scene=21#wechat_redirect)

[详解java类的生命周期](http://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247484796&idx=1&sn=c71933213a5435f3a7dfd1ddea34dfc8&chksm=ebd63a50dca1b346ed41498c71f11e1081a675d6f0d4a95e68325e57155cb44f2d1bf4e1efa7&scene=21#wechat_redirect)

[谈谈我对面向对象以及类与对象的理解](http://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247484958&idx=1&sn=2b233fb7edf92a8d49fc13b381e8a20d&chksm=ebd63932dca1b02478eb82b01e82a355f2bb6b94bfd220b036e2372701bd1f828c08ca4e06b3&scene=21#wechat_redirect)



**强引用、软引用、弱引用、虚引用与GC的关系**



强引用：new出的对象之类的引用，只要强引用还在，永远不会回收。

软引用：引用但非必须的对象，内存溢出异常之前回收。 

弱引用：非必须的对象，对象只能生存到下一次垃圾收集发生之前。 

虚引用：对生存时间无影响，在垃圾回收时得到通知。



这个相对好理解了，相关阅读如下：

[Java 如何有效地避免OOM：善于利用软引用和弱引用](http://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247484796&idx=2&sn=c3eda1000a5fc8e973d3a1ef242523c1&chksm=ebd63a50dca1b346ecefc62b403dcb3654b4c24379106ef25aad9759c492839666cac59fe324&scene=21#wechat_redirect)