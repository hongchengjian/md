# JDK 

在 HotSpot 主流 OS上，采用模板解释器执行字节码，与JIT 编译器一样，最终执行的汇编代码都是在运行时候产生，无法断点调试。HotSpot 增加了

-XX: +TraceBytecodes 

-XX: StopInterpreterAt=<n>

参数作用是遇序号为<n>的字节码指令时，便中断程序执行，中断程序执行，进入断点调试 

使用永久代 Permanent Generation 方法实现方法区  存在内存溢出问题-XX: MaxPermSize 上限，如32位系统中4GB限制

java -Xcomp 强制虚拟机运行编译模式 Compiled Mode

java -Xint 强制虚拟机运行解释模式 Interpreted Mode

## 逃逸分析

Escape Analysis分析对象动态作用域

方法逃逸：当一个对象在方法被定义后，它可能被外部方法所引用，e.g. 作为调用参数传递到其他地方中。

线程逃逸：当一个对象在方法被定义后，可能被外部线程访问，e.g.赋值给类变量或可以在其他线程中访问的实例变量。

开启逃逸分析：-XX:+DoEscapeAnalysis （JDK1.8之后默认开启）



## JDK 1.0.2

改动过 invokespecial 指令

## JDK 1.2

### 引入双亲委派模型

### 扩充引用

（1）强引用 Strong Referrence：Object obj = new Object();

（2）软引用 Soft Referrence：有用非必需对象如内存敏感的高速缓存，在系统将要发生内存溢出异常之前(内存不足时，就会回收），将进行第二次回收。

JDK 1.2之后，提供了 SoftReference 类。

（3）弱引用 Weak Refferrence：垃圾回收器工作时，无论内存是否足够，都会回收掉被弱引用关联的对象。

API 提供 WeakReference类实现canonicalizing mapping。

（4）虚引用Phantom Refferrence：无法通过虚引用获取一个对象实例，设置虚引用的目的是在这个对象被垃圾回收器回收时收到一个系统通知。

## JDK 1.4

NIO JSR 51：NIO优缺：引入 Channel 和  Buffer 的IO 方式，可以使用 Native 函数库直接分配堆外内存 ，然后通过一个存储在 Java 堆中的 DirectByteBuffer 对象作为这块内存的引用进行操作，从而避免了 Java 堆和 Native 堆中来回复制数据。

## JDK 1.5

### 引入两个新的reference types

（1）开始提供对注解 Annotation 的支持  annotation type

（2）enum type

枚举是类。Enums provide compile-time type safety。Enums are by their nature immutable。枚举是单例的。

## JDK 1.8

### Lambda

#### parallstream 遍历无序

```java
stream VS parallstream(Fork join分治Divide-and-Conquer Algorithm)
Collections.synchronizedList(new ArrayList<>()) 同步集合也只能保证元素都正确但无法保证其中的顺序。
    
采用并行流收集元素到集合中时，最好 collect(Collectors.tolist())是线程安全的。一定不要采用foreach或者map，foreach或map操作集合时会出现Null和数量不一致问题   
```

#### Stream分类

![JDK1.8 Stream](http://hongchengjian.gitee.io/md/img/jdk/JDK1.8%20Stream.png)

#### Stream原理

```java
public interface Stream<T> extends BaseStream<T, Stream<T>> 
public interface BaseStream<T, S extends BaseStream<T, S>> extends AutoCloseable 
```

#### Demo

```java
 Map<String, List<BudgetCompareRequest>> map = builder.getBudgetCompare().stream().collect(
                    Collectors.toMap(x -> String.valueOf(x.getCompanyId()), Lists::newArrayList,
                            (List<BudgetCompareRequest> newList, List<BudgetCompareRequest> oldList) -> {
                                oldList.addAll(newList);
                                return oldList;
                            }));


```



## 类的生命周期

lvpriuu

loading -> linking(verification -> preparation -> resolution) -> initialization -> using -> unloading

## GC分类

```
Young GC == Minor GC Eden占满时，新对象分配频率越高，Young GC频率越高
Young GC每次都Stop-The-World，暂停所有应用线程，停顿时间相对老年代GC停顿，几乎可以忽略不计。
Old GC: 只清理老年代GC、只有CMS并发收集是此模式
Full GC: 清理整个堆GC事件，包括新生代、老年代、元空间
Mixed GC: 清理整个新生代及部分老年代，只有G1有此模式
```

## GC日志分析

### 工具

GCViewer, gceasy

### 命令

```shell
-verbose:gc -XX:+PrintGCDetails -XX:+PrintGCDateStamps  -XX:+PrintGCTimeStamps
```



![](../../../MD/img/Young%20GC.png)



![](../../../MD/img/Full%20GC.png)



## Full GC(Major GC) 发生条件

发生条件老年代的连续空间 <（新生代所有对象的总大小或者历次晋升的平均大小）

-XX:+ DisableExplicitGC来禁止RMI（Java远程方法调用）调用System.gc( )

## Minor GC 发生条件

From Survior、To Survior互换时

## G1优势



## 什么时候发生

System.gc( )没人调用过

Full gc的过程是什么？

## Full GC VS Minor GC



## Minor GC会stop the world STW？

会

https://blogs.oracle.com/jonthecollector/our-collectors

## 调优

### 性能优化点

```css
过早优化会花费大量时间优化的是非关键部分
指定：为所有API指定最大响应时间、指定范围内导入记录数量
使用分析器来定位，凭空感觉会引入错误的方向 有哪些分析器？
定义生产环境的性能测试套件，在生产环境优化前、优化后运行它
java代码技巧：Ex. for中使用StringBuilder，注意StringBuilder中添加更多字符时，JVM将动态地改变StringBuilder的大小。若已经知道字符串包含多少字符，实例化一个具有被定义容量的StringBuilder提高它的效率。
StringBuilder sb = new StringBuilder(“This is a test”); 
for (int i=0; i<10; i++) { 
    sb.append(i); 
    sb.append(“”); 
} 
log.info(sb.toString());
注意：只是将一个字符串分解成多行来提高代码的可读性，用+连接，因为运行时，代码只使用1个字符，不需要连接。
Query q = em.createQuery(“SELECT a.id, a.firstName, a.lastName ” 
+ “FROM Author a”
+ “WHERE a.id = :id”);
尽最大可能使用primitive数据类型，JVM将它们存在Stack中，减少内存消耗
检查日志级别
if (log.isDebugEnabled()) { 
    log.debug(“User [” + userName + “] called method X with [” + i + “]”); 
}
Apache Commons Lang’s StringUtils.replace效率高于Java 8的String.replace https://blog.jooq.org/2017/10/11/benchmarking-jdk-string-replace-vs-apache-commons-stringutils-replace/
缓存资源、数据库链接 Integer类的valueOf方法缓存了- 128和127之间的值 
```

### PretenureSizeThreshold

-XX:PretenureSizeThreshold=3145728 定义多大的对象、长期存活的对象直接进入老年代

### JMM Java Memory Model

线程之间的共享变量存储在主内存 main memory，每一个线程都有一个私有本地内存 local memory，

本地内存中存储了该线程以读、写共享变量的副本。

### JVM是对Java内存模型的实现

### TProfile阿里开源在海量业务代码 精准定位性能代码问题

大量业务线程在频繁创建一些生命周期很长的临时对象

### OOM原因

（1）内存不足

（2）内存泄漏

### OOM可能发生在JVM哪些区域

PGen

Heap

Stack（VM Stack和Native Method Stack）

唯一不可能发生在程序计数器

### 如何排查OOM

Vmstat top找出最高的CPU、内存线程或jps —> heap dump分析—> MAT —> Leak suspect 对象集合中保存了大量对象的引用，导致内存泄露, 关注（1） while调用中new大对象（2）循环中建立大量连接调用（3） ThreadLoacl、流、资源、软引用对象、线程池是否用完回收和释放

### Full GC过程中Stop the World，JVM如何处理

Stop the World会暂停用户线程的执行

在GC发生时，直接把所有线程都挂起，然后检测所有线程是否都在安全点Safe Point，如果不在安全点则恢复线程的执行，等执行到安全点再挂起。

### Stop the World Minor GC也会发生

### 查看JVM默认参数

```java
 java -XX:+PrintCommandLineFlags -version
```



```java
C:\Users\DFG> java -XX:+PrintCommandLineFlags -version
-XX:InitialHeapSize=266719360 -XX:MaxHeapSize=4267509760 -XX:+PrintCommandLineFlags -XX:+UseCompressedClassPointers -XX:+UseCompressedOops -XX:-UseLargePagesIndividualAllocation -XX:+UseParallelGC
java version "1.8.0_251"
Java(TM) SE Runtime Environment (build 1.8.0_251-b08)
Java HotSpot(TM) 64-Bit Server VM (build 25.251-b08, mixed mode)
```

-XX:+UseCompressedOops 普通对象指针压缩 和 -XX:+UseCompressedClassPointers 类型指针压缩 默认开启，+代表开启，-代表关闭；Ex. Object o = new Object();中，o是Oop ordinary object pointer 普通对象指针，new Object()是ClassPointers，说明：这两个参数有四种组合++, --, + -, -+，其中-XX:+UseCompressedClassPointers -XX:-UseCompressedOops启动JVM会抛警告，不要使用这种参数组合



### JVM参数设置

```shell
-Xms250m	 堆初始值
-Xmx250m     堆最大值
-XX:MaxMetaspaceSize=50m 最大Metaspace大小，JDK1.8
```

```shell
C:\Users\DFG>jps
10788
23356 Jps
29628 GradleDaemon

C:\Users\DFG>jmap -heap 29628
Attaching to process ID 29628, please wait...
Debugger attached successfully.
Server compiler detected.
JVM version is 25.251-b08

using thread-local object allocation.
Parallel GC with 8 thread(s)

Heap Configuration:
   MinHeapFreeRatio         = 0
   MaxHeapFreeRatio         = 100
   MaxHeapSize              = 536870912 (512.0MB)
   NewSize                  = 89128960 (85.0MB)
   MaxNewSize               = 178782208 (170.5MB)
   OldSize                  = 179306496 (171.0MB)
   NewRatio                 = 2
   SurvivorRatio            = 8
   MetaspaceSize            = 21807104 (20.796875MB)
   CompressedClassSpaceSize = 260046848 (248.0MB)
   MaxMetaspaceSize         = 268435456 (256.0MB)
   G1HeapRegionSize         = 0 (0.0MB)

Heap Usage:
PS Young Generation
Eden Space:
   capacity = 85983232 (82.0MB)
   used     = 80051336 (76.34290313720703MB)
   free     = 5931896 (5.657096862792969MB)
   93.10110138683784% used
From Space:
   capacity = 44564480 (42.5MB)
   used     = 7830936 (7.468162536621094MB)
   free     = 36733544 (35.031837463378906MB)
   17.572147144990808% used
To Space:
   capacity = 44040192 (42.0MB)
   used     = 0 (0.0MB)
   free     = 44040192 (42.0MB)
   0.0% used
PS Old Generation
   capacity = 268435456 (256.0MB)
   used     = 245272384 (233.90997314453125MB)
   free     = 23163072 (22.09002685546875MB)
   91.37108325958252% used

22925 interned Strings occupying 2066632 bytes.


```



```shell
C:\Users\DFG>jps
10788
23356 Jps
29628 GradleDaemon
C:\Users\DFG>jstat -gc 29628
 S0C    S1C    S0U    S1U      EC       EU        OC         OU       MC     MU    CCSC   CCSU   YGC     YGCT    FGC    FGCT     GCT
43008.0 43520.0  0.0   7647.4 83968.0  81330.5   262144.0   239523.8  68736.0 65037.1 9344.0 8568.0     41    0.649   3      0.431    1.081


S0C、S1C、S0U、S1U：Survivor 0/1区容量（Capacity）和使用量（Used）
EC、EU：Eden区容量和使用量
OC、OU：年老代容量和使用量
PC、PU：永久代容量和使用量
YGC、YGT：年轻代GC次数和GC耗时
FGC、FGCT：Full GC次数和Full GC耗时
GCT：GC总耗时

```



```java
采样
C:\Users\DFG>jstat -gc 29628 1000
 S0C    S1C    S0U    S1U      EC       EU        OC         OU       MC     MU    CCSC   CCSU   YGC     YGCT    FGC    FGCT     GCT
43008.0 43520.0  0.0    0.0   87552.0   6251.6   297984.0   79807.8   69248.0 58706.0 9344.0 7731.9     42    0.685   4      0.802    1.488
43008.0 43520.0  0.0    0.0   87552.0   6251.6   297984.0   79807.8   69248.0 58706.0 9344.0 7731.9     42    0.685   4      0.802    1.488
43008.0 43520.0  0.0    0.0   87552.0   6251.6   297984.0   79807.8   69248.0 58706.0 9344.0 7731.9     42    0.685   4      0.802    1.488
43008.0 43520.0  0.0    0.0   87552.0   6251.6   297984.0   79807.8   69248.0 58706.0 9344.0 7731.9     42    0.685   4      0.802    1.488
43008.0 43520.0  0.0    0.0   87552.0   6558.5   297984.0   79807.8   69248.0 58706.0 9344.0 7731.9     42    0.685   4      0.802    1.488
```



```shell
jmap -histo 18095 | head -30 
jmap -histo:live <pid> | more 查看活跃对象
查看占用内存最大的对象
C:\Users\DFG>jmap -histo 29628

 num     #instances         #bytes  class name
----------------------------------------------
   1:       1098257      124517368  [C
   2:       1041581       24997944  java.lang.String
   3:        427877       20538096  com.sun.tools.javac.file.ZipFileIndex$Entry
   4:        110224       19301448  [B
   5:        392276       12552832  java.util.HashMap$Node
   6:        237744       11411712  java.util.HashMap
   7:         32739       10295928  [I
   8:        129604        9541760  [Ljava.lang.Object;
   9:        176183        7047320  com.sun.tools.javac.code.Scope$ImportScope$1
  10:        160427        6417080  java.util.HashMap$KeyIterator
  11:         32814        6130032  [Ljava.util.HashMap$Node;
  12:        192482        4619568  com.sun.tools.javac.util.List
  13:         46050        3684000  com.sun.tools.javac.code.Symbol$ClassSymbol
  14:        214067        3425072  java.util.HashSet
  15:         77266        3090640  java.util.LinkedHashMap$Entry
  16:         76566        3062640  org.gradle.api.internal.artifacts.dependencies.DefaultImmutableVersionConstraint
```



```java
(1)  D:\github>jmap -dump:format=b,file=D:\GhxcIcaApplicationDump.bat 4312
Dumping heap to D:\GhxcIcaApplicationDump.bat ...
Heap dump file created

(2)  C:\Users\DFG>jhat -port 8888 D:\GhxcIcaApplication.bat
Reading from D:\GhxcIcaApplication.bat...
Dump file created Mon Oct 12 17:08:09 CST 2020
Snapshot read, resolving...
Resolving 715261 objects...
Chasing references, expect 143 dots...............................................................................................................................................
Eliminating duplicate references...............................................................................................................................................
Snapshot resolved.
Started HTTP server on port 8888
Server is ready.

(3) browser : http://localhost:port 
其中 Object Query Language (OQL) query Ex. select s from java.lang.String s where s.value.length >= 1000 有什么用？
    
```

![OOL](../../../MD/img/image-20201029095227097.png)

```css
OQL语法： select <javascript expression to select>
[from [instanceof] <class name> <identifier>]
[where <javascript boolean expression to filter>]
 
Ex.
(1)查询长度大于100的字符串
select s from java.lang.String s where s.count > 100
(2)查询长度大于256的数组
select a from [I a where a.length > 256
(3)显示匹配某一正则表达式的字符串
select a.value.toString() from java.lang.String s where /java/(s.value.toString())
(4)显示所有文件对象的文件路径
select file.path.value.toString() from java.io.File file
(5)显示所有ClassLoader的类名
select classof(cl).name from instanceof java.lang.ClassLoader cl
(6)通过引用查询对象
select o from instanceof 0xd404d404 o

built-in对象 -- heap 
(1)heap.findClass(class name) -- 找到类
select heap.findClass("java.lang.String").superclass
(2)heap.findObject(object id) -- 找到对象
select heap.findObject("0xd404d404")
(3)heap.classes -- 所有类的枚举
select heap.classes
(4)heap.objects -- 所有对象的枚举
select heap.objects("java.lang.String")
(5)heap.finalizables -- 等待垃圾收集的java对象的枚举
(6)heap.livepaths -- 某一对象存活路径
select heaplivepaths(s) from java.lang.String s
(7)heap.roots -- 堆根集的枚举

辨识对象的函数 
(1)classof(class name) -- 返回java对象的类对象
select classof(cl).name from instanceof java.lang.ClassLoader cl
(2)identical(object1,object2) -- 返回是否两个对象是同一个实例
select identical(heap.findClass("java.lang.String").name, heap.findClass("java.lang.String").name)
(3)objectid(object) -- 返回对象的id
select objectid(s) from java.lang.String s
(4)reachables -- 返回可从对象可到达的对象
select reachables(p) from java.util.Properties p -- 查询从Properties对象可到达的对象
select reachables(u, "java.net.URL.handler") from java.net.URL u -- 查询从URL对象可到达的对象，但不包括从URL.handler可到达的对象
(5)referrers(object) -- 返回引用某一对象的对象
select referrers(s) from java.lang.String s where s.count > 100
(6)referees(object) -- 返回某一对象引用的对象
select referees(s) from java.lang.String s where s.count > 100
(7)refers(object1,object2) -- 返回是否第一个对象引用第二个对象
select refers(heap.findObject("0xd4d4d4d4"),heap.findObject("0xe4e4e4e4"))
(8)root(object) -- 返回是否对象是根集的成员
select root(heap.findObject("0xd4d4d4d4")) 
(9)sizeof(object) -- 返回对象的大小
select sizeof(o) from [I o
(10)toHtml(object) -- 返回对象的html格式
select "<b>" + toHtml(o) + "</b>" from java.lang.Object o
(11)选择多值
select {name:t.name?t.name.toString():"null",thread:t} from instanceof java.lang.Thread t

数组、迭代器等函数 
(1)concat(enumeration1,enumeration2) -- 将数组或枚举进行连接
select concat(referrers(p),referrers(p)) from java.util.Properties p
(2)contains(array, expression) -- 数组中元素是否满足某表达式
select p from java.util.Properties where contains(referres(p), "classof(it).name == 'java.lang.Class'")
返回由java.lang.Class引用的java.util.Properties对象
built-in变量
it -- 当前的迭代元素
index -- 当前迭代元素的索引
array -- 被迭代的数组
(3)count(array, expression) -- 满足某一条件的元素的数量
select count(heap.classes(), "/java.io./(it.name)")
(4)filter(array, expression) -- 过滤出满足某一条件的元素
select filter(heap.classes(), "/java.io./(it.name)")
(5)length(array) -- 返回数组长度
select length(heap.classes())
(6)map(array,expression) -- 根据表达式对数组中的元素进行转换映射
select map(heap.classes(),"index + '-->' + toHtml(it)")
(7)max(array,expression) -- 最大值, min(array,expression)
select max(heap.objects("java.lang.String"),"lhs.count>rhs.count")
built-in变量
lhs -- 左边元素
rhs -- 右边元素
(8)sort(array,expression) -- 排序
select sort(heap.objects('[C'),'sizeof(lhs)-sizeof(rhs)')
(9)sum(array,expression) -- 求和
select sum(heap.objects('[C'),'sizeof(it)')
(10)toArray(array) -- 返回数组
(11)unique(array) -- 唯一化数组
```



### jstack 关注线程状态，分析线程执行情况

```
C:\Users\DFG>jstack 4312
2020-10-12 17:19:35
Full thread dump Java HotSpot(TM) 64-Bit Server VM (25.251-b08 mixed mode):

"SimplePauseDetectorThread_2" #76 daemon prio=5 os_prio=0 tid=0x000000002060c000 nid=0x3500 waiting on condition [0x000000002820f000]
   java.lang.Thread.State: TIMED_WAITING (sleeping)
        at java.lang.Thread.sleep(Native Method)
        at java.lang.Thread.sleep(Thread.java:340)
        at java.util.concurrent.TimeUnit.sleep(TimeUnit.java:386)
        at org.LatencyUtils.TimeServices.sleepNanos(TimeServices.java:62)
        at org.LatencyUtils.SimplePauseDetector$SimplePauseDetectorThread.run(SimplePauseDetector.java:116)

"SimplePauseDetectorThread_1" #75 daemon prio=5 os_prio=0 tid=0x0000000020607000 nid=0x7bfc waiting on condition [0x000000002810e000]
   java.lang.Thread.State: TIMED_WAITING (sleeping)
        at java.lang.Thread.sleep(Native Method)
        at java.lang.Thread.sleep(Thread.java:340)
        at java.util.concurrent.TimeUnit.sleep(TimeUnit.java:386)
        at org.LatencyUtils.TimeServices.sleepNanos(TimeServices.java:62)
        at org.LatencyUtils.SimplePauseDetector$SimplePauseDetectorThread.run(SimplePauseDetector.java:116)

"SimplePauseDetectorThread_0" #74 daemon prio=5 os_prio=0 tid=0x000000001f543800 nid=0x6228 waiting on condition [0x000000002800e000]
   java.lang.Thread.State: TIMED_WAITING (sleeping)
        at java.lang.Thread.sleep(Native Method)
        at java.lang.Thread.sleep(Thread.java:340)
        at java.util.concurrent.TimeUnit.sleep(TimeUnit.java:386)
        at org.LatencyUtils.TimeServices.sleepNanos(TimeServices.java:62)
        at org.LatencyUtils.SimplePauseDetector$SimplePauseDetectorThread.run(SimplePauseDetector.java:116)
```



### 分析内存或CPU占用高



### jmap查看内存泄漏

# 