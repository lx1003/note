## JVM运行时数据区

程序计数器

字节码解释器工作时通过改变这个计数器的值来选取下一条需要执行的字节码指令、分支、循环、跳转、异常处理、线程恢复等功能都需要以来这个计数器来完

为了线程切换后恢复到正确的执行位置，每条线程都需要有一个独立的程序计数器，各线程之间计数器互不影响、独立存储，我们称这类内存区域为“线程私有”的内存。

1. 字节码解释器通过改变程序计数器来依次读取指令，从而实现代码的流程控制
2. 在多线程的情况下，程序计数器用于记录当前线程执行的位置，从而当线程被切换回来的时候能够知道该线程上次运行到哪了
3. 程序计数器是唯一一个不会出现OutOfMemoryError的内存区域，它的生命周期随着线程的创建而创建，随着线程的结束而死亡

## Java虚拟机栈

与程序计数器一样，Java虚拟机栈也是线程私有的，它的生命周期和线程相同，描述的是Java方法执行的内存模型，每次方法调用的数据都是通过栈传递的

Java内存可以粗糙的区分堆内存和栈内存，其中栈就是现在说的虚拟机栈，或者说是虚拟机栈中局部变量表部分

局部变量表主要存放了编译器可知的各种数据类型、对象的引用

StackOverflowError和OutOfMemoryError

Java虚拟机栈也是线程私有的，每个线程都有各自的Java虚拟机栈，而且随着现成的创建而创建，随着线程的死亡而死亡

## 本地方法栈

和虚拟机栈所发挥的作用非常相似，区别是：虚拟机栈为虚拟机执行Java方法服务，而本地方法栈则为虚拟机使用到的Native方法服务

本地方法被执行的时候，在本地方法栈也会创建一个栈帧，用于存放该本地方法的局部变量表、操作数栈、动态链接、出口信息

方法执行完毕后相应的栈帧也会出栈并释放内存空间，也会出现StackOverFlowError和OutOfMemoryError两种异常

## 堆

Java虚拟机所管理的内存中最大的一块，Java堆是所有线程共享的一块内存区域，在虚拟机启动时创建。此内存区域的唯一目的就是存放对象实例，几乎所有的对象实例以及数据都在这里分配内存

Java堆是垃圾收集器管理的主要区域，因此也被称为GC堆。从垃圾回收的角度，由于现在收集器基本都采用分代垃圾收集算法，所以Java堆还可以细分为：新生代和老年代

![image-20200415153538094](C:\Users\XN\AppData\Roaming\Typora\typora-user-images\image-20200415153538094.png)

1. 类加载检查：虚拟机遇到一条new指令时，首先将去检查这个指令的参数是否能在常量池中定位到这个类的符号引用，并且检查这个符号引用代表的类是否已被加载过、解析和初始化过。如果没有，那必须先执行相应的类加载过程
2. 分配内存：在类加载检查通过后，接下来虚拟机将为新生对象分配内存。对象所需的内存大小在类加载完成后便可确定，为对象分配空间的任务等同于把一块确定大小的内存从Java堆中划分出来。分配方式有“指针碰撞”和“空间列表”两种，选择那种分配方式是由Java堆是否规整决定，而Java堆是否规整又由所采用的垃圾收集器是否带有压缩整理功能决定