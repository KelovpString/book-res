## Jvm 简介

Jvm（Java Virtual Machine）是可运行Java代码的假想计算机，包括字节码指令集、一组寄存器、一个栈、一个垃圾会收集、堆、存储方法域。Jvm是运行在操作系统之上的，和硬件没有直接的交互。而Java 的源文件可以通过编译器产生相应的class文件（字节码文件），用虚拟机中的解释器编译成特定机器上的机器码，即：

> .java -> 编译器 -> 字节码文件 ->JVM ->机器码

由于不同平台的解释器是不同的，实现的虚拟机却是相同的，这也是Java为何具有跨平台特性的原因。当一个程序开始运行，虚拟机就开始实例化，多个程序启动就会存在多个虚拟机实例，程序退出或者关闭，虚拟机实例就会消亡，多个虚拟机实例之间的数据是不能共享的。在运行时，一般虚拟机的结构如下：

> a. 运行时数据区：
>   1. 方法区
>   2. 栈
>   3. 虚拟机栈
>   4. 本地方法栈
>   5. 程序计数器 

> b. 执行引擎
>  1. 即时编译器
>  2. 垃圾回收

> c. 本地库接口-> d.本地方法库

而类加载器子系统操作运行时数据区的内容。

Jvm的作用即完成java代码的执行、实现内存管理、控制线程资源同步和提供交互机制
其中Java代码的执行流程为：

> 代码由javac 编译为.class文件 -> classLoader 完成类装载 ->解释器完成解释执行 -> 编译器完成编译优化（Client/Server Compiler）->执行

在内存管理这块（JMM）主要是进行对内存空间的一些操作，涵盖分配、回收，Jvm也提供了一些内存状况的分析工具（jstat/jmap/visualvm/jconsole）

而后面线程资源同步的部分由具体的jdk当中的java类实现的一些线程资源同步（Lock/Synchronized）,交互则有JUC下的部分类和Object下的类控制