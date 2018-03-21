JVM的内存结构

根据 JVM 规范，JVM 内存共分为虚拟机栈、堆、方法区、程序计数器、本地方法栈五个部分。



1、Java虚拟机栈：

线程私有；每个方法在执行的时候会创建一个栈帧，存储了局部变量表，操作数栈，动态连接，方法返回地址等；每个方法从调用到执行完毕，对应一个栈帧在虚拟机栈中的入栈和出栈。



2、堆：

线程共享；被所有线程共享的一块内存区域，在虚拟机启动时创建，用于存放对象实例。



3、方法区：

线程共享；被所有线程共享的一块内存区域；用于存储已被虚拟机加载的类信息，常量，静态变量等。



4、程序计数器：

线程私有；是当前线程所执行的字节码的行号指示器，每条线程都要有一个独立的程序计数器，这类内存也称为“线程私有”的内存。



5、本地方法栈：

线程私有；主要为虚拟机使用到的Native方法服务。



大体回答如上，类似文章请移驾：

[JVM的内存区域划分](http://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247484719&idx=1&sn=c0f3a3d518dd89a08acad5f0ef0cdca6&chksm=ebd63a03dca1b315cf60bbdcd034ad22d5a0c1afe194d185fe0cf5b19ce15fb3e70630f3c9b9&scene=21#wechat_redirect)

[JVM知识点梳理](http://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247484237&idx=1&sn=79d99a5bc17453e5cdd3ca1f9ad97d13&chksm=ebd63c61dca1b5776136bf20f63e4654facf4e025e9ef01d94c7662a8916613fc86d345d3307&scene=21#wechat_redirect)

[JVM内存分配与回收](http://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247484011&idx=1&sn=2efb8e99d2ce18b6a8f640978c09ab16&chksm=ebd63d47dca1b4516161db13f20e8ef3cc2b3c055fbb06ca81e92fa5cf96215304a3067ce5c7&scene=21#wechat_redirect)

[JVM内存管理机制](http://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247484008&idx=1&sn=64340424e740f49329e9ed0ea58c03f6&chksm=ebd63d44dca1b452a491c76d088305fcb4b9ab50c29596dc3bb7941139cd6b31057a5f21900e&scene=21#wechat_redirect)






**强引用，软引用和弱引用的区别**

强引用：

只有这个引用被释放之后，对象才会被释放掉，只要引用存在，垃圾回收器永远不会回收，这是最常见的New出来的对象。



软引用：

内存溢出之前通过代码回收的引用。软引用主要用户实现类似缓存的功能，在内存足够的情况下直接通过软引用取值，无需从繁忙的真实来源查询数据，提升速度；当内存不足时，自动删除这部分缓存数据，从真正的来源查询这些数据。



弱引用：

第二次垃圾回收时回收的引用，短时间内通过弱引用取对应的数据，可以取到，当执行过第二次垃圾回收时，将返回null。弱引用主要用于监控对象是否已经被垃圾回收器标记为即将回收的垃圾，可以通过弱引用的isEnQueued方法返回对象是否被垃圾回收器标记。


大体回答如上，类似文章请移驾：

[Java 如何有效地避免OOM：善于利用软引用和弱引用](http://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247484796&idx=2&sn=c3eda1000a5fc8e973d3a1ef242523c1&chksm=ebd63a50dca1b346ecefc62b403dcb3654b4c24379106ef25aad9759c492839666cac59fe324&scene=21#wechat_redirect)





**数组在内存中如何分配**

1、简单的值类型的数组，每个数组成员是一个引用（指针），引用到栈上的空间（因为值类型变量的内存分配在栈上）

2、引用类型，类类型的数组，每个数组成员仍是一个引用（指针），引用到堆上的空间（因为类的实例的内存分配在堆上）





**用过哪些设计模式，手写一个（除单例）**

[设计模式早有总结，看这里：23种设计模式完整总结](http://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247484804&idx=1&sn=108f79096a2cdd77996e7c2a4d337b8f&chksm=ebd63aa8dca1b3bec6cf720c9d0f4487fcf957aab1f43312fe6d9b59df2feae92aeacc967ed2&scene=21#wechat_redirect)




**springmvc的核心是什么，请求的流程是怎么处理的，控制反转怎么实现的**

核心：

控制反转和面向切面



请求处理流程：

1、首先用户发送请求到前端控制器，前端控制器根据请求信息（如URL）来决定选择哪一个页面控制器进行处理并把请求委托给它，即以前的控制器的控制逻辑部分；

2、页面控制器接收到请求后，进行功能处理，首先需要收集和绑定请求参数到一个对象，并进行验证，然后将命令对象委托给业务对象进行处理；处理完毕后返回一个ModelAndView（模型数据和逻辑视图名）；

3、前端控制器收回控制权，然后根据返回的逻辑视图名，选择相应的视图进行渲染，并把模型数据传入以便视图渲染；

4、前端控制器再次收回控制权，将响应返回给用户。



控制反转如何实现：

我们每次使用spring框架都要配置xml文件，这个xml配置了bean的id和class。

spring中默认的bean为单实例模式，通过bean的class引用反射机制可以创建这个实例。

因此，spring框架通过反射替我们创建好了实例并且替我们维护他们。

A需要引用B类，spring框架就会通过xml把B实例的引用传给了A的成员变量。



大体回答如上，类似文章请移驾：

[理解Spring中的IOC和AOP](http://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247484436&idx=1&sn=76f65083024334a5f068f9796e8cf224&chksm=ebd63b38dca1b22e03bb3859006902ae7df8385970e6b64c1066741e27d8a636ffb3ed7333c9&scene=21#wechat_redirect)



**spring里面的aop的原理是什么**

这个有介绍，看这里：[Spring的IOC原理](http://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247484851&idx=2&sn=178ec1bf904471a846b6457e4a27e0b8&chksm=ebd63a9fdca1b3899276a9be3bf0d889f541ddbcc6a965423a6b036be5f0c4a013b7f94b2cec&scene=21#wechat_redirect)




**mybatis如何处理结果集**

MyBatis的结果集是通过反射来实现的。并不是通过get/set方法。在实体类中无论是否定义get/set()方法，都是可以接收到的。



如果面试只是考你这个点的话就恭喜了。如果继续深问流程，那就需要自己找一些源码来阅读了。





**java的多态表现在哪里**

主要有两种表现形式：重载和重写


重载：

是发生在同一类中，具有相同的方法名，主要是看参数的个数，类型，顺序不同实现方法的重载的，返回值的类型可以不同。



重写：

是发生在两个类中（父类和子类），具有相同的方法名，主要看方法中参数，个数，类型必须相同，返回值的类型必须相同。



大体回答如上，类似文章请移驾：

[面向对象之多态【向上转型与向下转型】](http://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247484902&idx=1&sn=aebf8fcfedf9182f30348a86926e6a3b&chksm=ebd63acadca1b3dc184dad42f865b482ba9958f3fa9a070ccda0ac51a53bca55235ca4fc6b48&scene=21#wechat_redirect)