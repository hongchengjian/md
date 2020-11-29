作者：cj  

# 线程

extends Thread Java中类仅单继承，Java中接口可多继承

Implements Runnable 方便一组线程访问相同资源，避免Thread创建多对象的内存浪费。

Callable 有返回值可获取Future(Future用于接收返回的结果，Future#get( )一直阻塞到获取到结果)，Runnable无返回值。注意Future若漏掉返回值为空时会导致程序阻塞。

## JAVA API-线程状态State 枚举

NEW、RUNNABLE、BLOCKED、WAITING、TIMED_WAITING、TERMINATED

```java
  /**
     * A thread state.  A thread can be in one of the following states:
     * <ul>
     * <li>{@link #NEW}<br>
     *     A thread that has not yet started is in this state.
     *     </li>
     * <li>{@link #RUNNABLE}<br>
     *     A thread executing in the Java virtual machine is in this state.
     *     </li>
     * <li>{@link #BLOCKED}<br>
     *     A thread that is blocked waiting for a monitor lock
     *     is in this state.
     *     </li>
     * <li>{@link #WAITING}<br>
     *     A thread that is waiting indefinitely for another thread to
     *     perform a particular action is in this state.
     *     </li>
     * <li>{@link #TIMED_WAITING}<br>
     *     A thread that is waiting for another thread to perform an action
     *     for up to a specified waiting time is in this state.
     *     </li>
     * <li>{@link #TERMINATED}<br>
     *     A thread that has exited is in this state.
     *     </li>
     * </ul>
     *
     * <p>
     * A thread can be in only one state at a given point in time.
     * These states are virtual machine states which do not reflect
     * any operating system thread states.
     *
     * @since   1.5
     * @see #getState
     */
    public enum State {
        /**
         * Thread state for a thread which has not yet started.
         */
        NEW,

        /**
         * Thread state for a runnable thread.  A thread in the runnable
         * state is executing in the Java virtual machine but it may
         * be waiting for other resources from the operating system
         * such as processor.
         */
        RUNNABLE,

        /**
         * Thread state for a thread blocked waiting for a monitor lock.
         * A thread in the blocked state is waiting for a monitor lock
         * to enter a synchronized block/method or
         * reenter a synchronized block/method after calling
         * {@link Object#wait() Object.wait}.
         */
        BLOCKED,

        /**
         * Thread state for a waiting thread.
         * A thread is in the waiting state due to calling one of the
         * following methods:
         * <ul>
         *   <li>{@link Object#wait() Object.wait} with no timeout</li>
         *   <li>{@link #join() Thread.join} with no timeout</li>
         *   <li>{@link LockSupport#park() LockSupport.park}</li>
         * </ul>
         *
         * <p>A thread in the waiting state is waiting for another thread to
         * perform a particular action.
         *
         * For example, a thread that has called <tt>Object.wait()</tt>
         * on an object is waiting for another thread to call
         * <tt>Object.notify()</tt> or <tt>Object.notifyAll()</tt> on
         * that object. A thread that has called <tt>Thread.join()</tt>
         * is waiting for a specified thread to terminate.
         */
        WAITING,

        /**
         * Thread state for a waiting thread with a specified waiting time.
         * A thread is in the timed waiting state due to calling one of
         * the following methods with a specified positive waiting time:
         * <ul>
         *   <li>{@link #sleep Thread.sleep}</li>
         *   <li>{@link Object#wait(long) Object.wait} with timeout</li>
         *   <li>{@link #join(long) Thread.join} with timeout</li>
         *   <li>{@link LockSupport#parkNanos LockSupport.parkNanos}</li>
         *   <li>{@link LockSupport#parkUntil LockSupport.parkUntil}</li>
         * </ul>
         */
        TIMED_WAITING,

        /**
         * Thread state for a terminated thread.
         * The thread has completed execution.
         */
        TERMINATED;
    }
```

## 线程状态流转

![Thread](http://hongchengjian.gitee.io/md/img/thread/Thread.png)

## 线程开始

start( )而非run( )，run是Runable接口的一个@Overwrite的方法

```java
@FunctionalInterface
public interface Runnable {
    /**
     * When an object implementing interface <code>Runnable</code> is used
     * to create a thread, starting the thread causes the object's
     * <code>run</code> method to be called in that separately executing
     * thread.
     * <p>
     * The general contract of the method <code>run</code> is that it may
     * take any action whatsoever.
     *
     * @see     java.lang.Thread#run()
     */
    public abstract void run();
}
```

## 线程结束

（1）正常main、call、run方法结束

（2）interrupt捕获异常java.lang.InterruptedException: sleep interrupted 时，break跳出 

待补充其他结束方式

## Java API-常用方法

### @Deprecated Thread.stop, Thread.suspend, Thread.resume

```css
Thread.stop( )线程不安全，会释放子线程所有锁，被保护的数据有可能呈现不一致性，导致错误。
```

### 对象锁

#### 什么是对象锁？

对象锁是指Java为临界区 synchronized(obj)指定的对象obj进行加锁，对象锁是独占锁(排他锁)。

对象锁用于程序片段或者method上，此时将获得对象的锁，所有想要进入该对象synchronized的方法或者代码段的线程都必须获取对象的锁，如果没有，则必须等其他线程释放该锁。

#### 私有对象锁避免客户端拒绝服务攻击

```java
// private lock object idiom - thwarts denial-of-service attack
// final防止不小心改变它的内容，而破坏锁对象
	private final Object lock = new Object();
 // 注：static 修饰与程序有相同生命周期的变量，在程序执行前就分配了内存，运行时不再改变内存分配情况
	public void foo() {
		synchronized (lock) {
			...
		}
	}

适用场景：专为继承而设计的类，不然子类和父类很可能相互锁住对方。
```

### Object.wait( ) 、Object.notify( ) 、Object.notifyAll( )

Object.wait( )  会释放对象锁。

SAP面试题-Object.wait( ) 调用的外层代码没有锁时，会发生什么？编译不报错，但是运行报错java.lang.IllegalMonitorStateException。

```java
public class TestWait {
    public static void main(String[] args) throws InterruptedException {
        TestWait wait = new TestWait();
        wait.wait();
    }
}

Exception in thread "main" java.lang.IllegalMonitorStateException
	at java.lang.Object.wait(Native Method)
	at java.lang.Object.wait(Object.java:502)
	at org.union.czt.test.TestWait.main(TestWait.java:7)
```

Object.notify( ) 唤醒Object Monitor(对象监视器)上的任一等待的单个线程。如果有多个等待线程有竞争吗？是随机唤醒吗？

Javadoc 对 notify( )方法说明

```java
Wakes up a single thread that is waiting on this object's monitor. If any threads are waiting on this object, one of them is chosen to be awakened. The choice is arbitrary and occurs at
the discretion of the implementation. 
```

证明唤醒的顺序是无序

```java
package main.java.thread;

import java.util.LinkedList;
import java.util.List;

public class TestNotifyOrder {
    /**
     * 对象锁
     */
    private final Object object = new Object();

    private List<Integer> sleepList = new LinkedList<>();
    private List<Integer> notifyList = new LinkedList<>();

    /**
     * 该线程作为一个唤醒线程
     */
    public void startThread(int i) {
        Thread t = new Thread(new Runnable() {
            @Override
            public void run() {
                synchronized (object) {
                    try {
                        System.out.println(Thread.currentThread().getName() + "进入休眠");
                        sleepList.add(i);
                        object.wait();
                        // 下面的代码线程被唤醒时才执行
                        System.out.println(Thread.currentThread().getName() + "线程已经唤醒");
                        notifyList.add(i);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            }
        });
        // 设置当前线程名
        t.setName("Thread" + i);
        t.start();
    }

    public static void main(String[] args) {
        TestNotifyOrder a = new TestNotifyOrder();
        // 21个线程实际运行的顺序是不固定的
        for (int i = 1; i < 22; i++) {
            a.startThread(i);
        }

        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println();
        // 每次被唤醒的线程也是21个线程中随机的一个
        for (int i = 1; i < 22; i++) {
            synchronized (a.object) {
                a.object.notify();
            }
        }

        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("休眠顺序" + a.sleepList);
        System.out.println("唤醒顺序" + a.notifyList);
    }
}

```

Object.notifyAll( )唤醒Object Monitor(对象监视器)上等待的所有线程，继续执行下去；

Thread.sleep(long) 线程的sleep时间结束后是进入runnable还是running状态？ runnable。

### Thread.sleep(long) VS Object.wait( )  VS  Object.wait(long )

Thread.sleep(long) 不改变锁行为，若当前线程拥有锁，Thread.sleep(long) 并不会释放锁。

调用 Object.wait( ) 后，需要别的线程执行Object.notify/notifyAll才能够重新获得CPU执行时间。注意是别的线程，调用 Object.wait( )的线程再调Object.notify/notifyAll是不行的。

共同点：Thread.sleep(long) 和 Object.wait(long)  都是使线程 RUNNABLE -> TIMED_WAITING，时间结束都是回到RUNNABLE 状态。Thread.sleep(long)时间结束还是继续执行当前线程后续逻辑。

### Thread.sleep(long)  VS Thread.yield( ) 

Thread.yield( ) 使线程 running -> runable，当前线程和其他线程有竞争关系，进入runnable的线程不一定是当前线程，有可能是其他线程。Thread.sleep(long)时间到了一定是当前线程进入runnable状态。

Thread.join( ) 主线程等子线程执行结束后再执行。

Thread.interrupt( )作用不是中断线程，而是通知线程应该中断了，具体中断还是继续运行，由被通知的线程自己处理。

### 判断线程有没有持有对象锁Thread.holdsLock(obj)

Thread.holdsLock(obj)持有monitor lock返回true

### 控制线程执行顺序Thread.join( )和多线程的无序执行

```java
main(){
		thread1();
		thread2();
}
// 3个线程：虽然代码顺序是Main、thread1、thread2，但创建三个线程后，竞争抢CPU时间片，谁先执行完是不确定的。

main() {
    thread1.start();
    thread1.join();
    thread2.start();
    thead2.join();
    thread3.start();
}
```

### 守护线程（服务线程）setDaemon( )

```java
thread = new Thread(this);
thread.setDaemon(true);
thread.start();
```

优先级低，为系统其他对象和线程提供服务，可做实时监控、管理系统，最好守护线程不要写影响业务逻辑。

垃圾回收GC线程是一个守护线程，当JVM中没有非守护线程在运行时，Java虚拟机会关闭。当所有常规线程运行完毕后，守护线程不管运行到哪里都会退出运行。

# 线程池

## 原理和流程

![ThreadPool](http://hongchengjian.gitee.io/md/img/thread/ThreadPool.png)

说明：当线程数小于核心线程数，即使有空闲线程，线程池也会创建新线程处理。

线程数>= corePoolSize，且任务队列已满，线程池会创建新线程来处理任务。

线程数=maxPoolSize，且任务队列已满，线程池会拒绝处理任务而抛异常。

![ThreadPool Model](http://hongchengjian.gitee.io/md/img/thread/ThreadPool%20Model.png)

## 线程池 VS new Thread

### new Thread缺陷 

创建对象性能差，缺统一管理，缺定时等功能。直接new多个thread在大并发下因系统缺少资源运行可能会丢失部分，而线程池可以充分管理线程，调度资源。

### Executors创建线程池缺陷

阿里发布的 Java开发手册中强制线程池不允许使用 Executors 去创建，而是通过 ThreadPoolExecutor 的方式。

Executors创建的线程池存在OOM两种情况，（1）maximumPoolSize传的是Integer.MAX_VALUE

比如newCachedThreadPool、newScheduledThreadPool，创建线程需要大量资源

（2）LinkedBlockingQueue是一个用链表实现的有界阻塞队列，不设置是一个无边界的阻塞队列，最大长度为Integer.MAX_VALUE，原因是高并发下，线程数达到maximumPoolSize时处理不过来任务，任务往LinkedBlockingQueue放，LinkedBlockingQueue无界一直放任务耗光系统内存

比如newFixedThreadPool、newSingleThreadExecutor

```java
// 验证高并发下OOM
public class TestExecutorService {
    // private static ExecutorService executor = Executors.newFixedThreadPool(2);
    private static ExecutorService executor = Executors.newSingleThreadExecutor();

    //向kafka里推送消费
    public static void doSth(Object msg) {
        executor.execute(() -> {
            try {
                //模拟 占用的内存大小
                Byte[] bytes = new Byte[1024 * 1000 * 1000];
                System.out.println(Thread.currentThread().getName() + "-->任务放到线程池:" + msg);
                TimeUnit.MINUTES.sleep(1);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });
    }

    public static void main(String[] args) {
        //模拟高并发环境下  一直向线程池里面不停的塞任务
        for (int i = 0; i < 10000; i++) {
            System.out.println("塞任务start..." + i);
            doSth(i);
            System.out.println("塞任务end..." + i);
        }
    }
}


// console
塞任务end...2249
塞任务start...2250
塞任务end...2250
塞任务start...2251
塞任务end...2251
塞任务start...2252
塞任务end...2252
Exception in thread "pool-1-thread-79" java.lang.OutOfMemoryError: Java heap space
```



## Java API-线程池 Executor实现对比

newCacheThreadExecutor（短期异步short-lived asynchronous tasks、有可用线程可用直接复用，无可用线程则创建新的线程并加到池子里。空闲60s的线程(60s未使用)会被移除）

```java
    // a pool that remains idle for long enough will not consume any resources
    public static ExecutorService newCachedThreadPool() {
        return new ThreadPoolExecutor(0, Integer.MAX_VALUE,
                                      60L, TimeUnit.SECONDS,
                                      new SynchronousQueue<Runnable>());
    }
```

newFixedThreadPool（定长线程池，可用固定数量线程数、共享无界队列a shared unbounded queue、超时不会自动关闭）

```java
//  The threads in the pool will exist until it is explicitly {@link ExecutorService#shutdown}
public static ExecutorService newFixedThreadPool(int nThreads) {
    // LinkedBlockingQueue是一个用链表实现的有界阻塞队列，不设置是一个无边界的阻塞队列，最大长度为Integer.MAX_VALUE
    // corePoolSize == maximumPoolSize == nThreads
        return new ThreadPoolExecutor(nThreads, nThreads,
                                      0L, TimeUnit.MILLISECONDS,
                                      new LinkedBlockingQueue<Runnable>());
    }
```

newScheduledThreadPool（支持定时或周期性任务执行）

```java
    public ScheduledThreadPoolExecutor(int corePoolSize) {
        super(corePoolSize, Integer.MAX_VALUE, 0, NANOSECONDS,
              new DelayedWorkQueue());
    }
```

newSingleThreadExecutor（单线程串行化的线程池，用唯一的工作线程来执行任务，任务是按指定顺序（FIFO、LIFO、优先级）执行。

```java
    public static ExecutorService newSingleThreadExecutor() {
        return new FinalizableDelegatedExecutorService
            (new ThreadPoolExecutor(1, 1,
                                    0L, TimeUnit.MILLISECONDS,
                                    new LinkedBlockingQueue<Runnable>()));
    }
```



## 正确创建线程池

（1）使用Guava提供的ThreadFactoryBuilder来创建线程池，为什么Guava不会溢出？

```java
public class Demo {

    private static ThreadFactory nameFactory = new ThreadFactoryBuilder()
        .setNameFormat("demo-pool-%d").build();

    // LinkedBlockingQueue是一个用链表实现的有界阻塞队列，不设置是一个无边界的阻塞队列，最大长度为Integer.MAX_VALUE
    private static ExecutorService pool = new ThreadPoolExecutor(5, 200,
        0L, TimeUnit.MILLISECONDS,
        new LinkedBlockingQueue<Runnable>(1024), namedFactory, new ThreadPoolExecutor.AbortPolicy());

    public static void main(String[] args) {

        for (int i = 0; i < Integer.MAX_VALUE; i++) {
            pool.execute(new SubThread());
        }
    }
}
```

（2）给BlockQueue指定容量private static ExecutorService executor = new ThreadPoolExecutor(10, 10, 60L, TimeUnit.SECONDS,new ArrayBlockingQueue(10));一旦提交的线程数超过当前可用线程数时，就会抛出java.util.concurrent.RejectedExecutionException。

## 线程池四要素

线程池四要素（1）池子管理器（作用是创建池子）（2）工作线程数（3）任务接口（4）队列

## 线程池参数

线程池：corePoolSize、maxiumPoolSize、keepaliveTime、workQueue、handler

## 线程池参数默认值

corePoolSize = 1

queueCapacity = Integer.MAX_VALUE

maxPoolSize=Integer.MAX_VALUE

keepAliveTime=60s

allowCoreThreadTimeout=false

rejectedExcutionHandler=AbortPolicy( )

## 线程池参数经验值设置（实际看生产机器）

tasks：每秒的任务数，假设为500~1000

taskCost：每个任务需要花费的时间，假设为0.1s

responseTime：系统允许的最大响应时间，假设为2s

corePoolSize = tasks * taskCost ( s为单位 )= (500~1000)*0.1= 50~100个线程。corePoolSize的个数应该大于等于50。根据8020原则，如果每秒80%的时间执行200个任务，corePoolSize设置为80即可。

queueCapacity = corePoolSize * taskCost * responseTime

为了将线程数只会保持在corePoolSize大小，当任务陡增时，不会开新的线程来执行，responseTime也会陡增。

maxPoolSize =  (max(tasks)-queueCapacity) * taskCost 

机器横向扩展、CPU核数预估

**CPU密集型任务**，尽量压榨CPU， NCPU+1

**IO密集型任务**，2*NCPU

## JOL工具线程池根据CPU核数初始化线程池

```java
ExecutorService threadPool = Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors());
```

## 验证线程池参数经验值设定效果

压测工具sysbench 	https://blog.csdn.net/IThelei/article/details/98126187

## 线程池拒绝策略4种与扩展

（1）Abort Policy抛异常阻止运行

（2）CallerRuns Policy跑当前被丢弃的任务

（3）Discard Oldest Policy 丢弃最老的请求

（4）Discard Policy丢弃无法处理的请求任务

线程拒绝策略自定义实现 implements RejectedExecutionHandler

## 线程池自动关闭

（1）corePoolSize设置为0，keepAliveTime指定一个long值，线程池在空闲一段时间后会自动关闭。

（2）allowCoreThreadTimeOut(true)设置为true，核心线程数corePoolSize也受keepAliveTime控制。

## 线程池任务在收到某个事件后关闭其中一个线程，其他线程继续执行

（1）开关

```java
public class MyThread extends Thread {
    public volatile boolean exit = false; 
        public void run() { 
        while (!exit){
            //do something
        }
    } 
```

（2）一个线程在运行状态中，中断标志被设置为true后，一旦线程调用了Thread.sleep( )、Object.wait( )、BlockingQueue.put( )、BlockingQueue.take( )方法中的一种，立马抛出一个InterruptedException（进行异常捕获+break退出)，且中断标志被清除，重新设置为false。

```java
public class ThreadTest {
 
    static class MyThread extends Thread {
        @Override
        public void run() {
            while (!isInterrupted()){ //非阻塞过程中通过判断中断标志来退出
                try{
                    Thread.sleep(5*1000);//阻塞过程捕获中断异常来退出
                }catch(InterruptedException e){
                    e.printStackTrace();
                    System.out.println("ThreadSafe:run()"+e.getMessage());
                    break;//捕获到异常之后，执行break跳出循环。
                }
            }
        }
    }
 
    public static void main(String[] args) throws Exception {
        Thread thread = new ThreadSafe();
        thread.start();
        System.out.println("在50秒之内按任意键中断线程!");
        System.in.read();
        thread.interrupt();
        Thread.sleep(5000);
        System.out.println("线程已经退出!thread.is" + thread.isAlive());
    }
}
```

## 线程中断响应

在JVM中，每个线程都有一个与之关联的Boolean属性，被称之为中断状态，可以通过Thread.currentThread( ).isInterrupted( )来获取当前线程的中断状态，初始值为false。

当线程正在执行这些方法时，被其他线程中断掉，该线程会首先清除掉中断状态（设置中断属性为false），然后抛出InterruptedException异常。

```java
public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(() -> {
            try {
                System.out.println("线程初始中断状态 -> " + Thread.currentThread().isInterrupted());
                Thread.sleep(10000);
            } catch (InterruptedException e) {
                System.out.println("抛出异常后线程中断状态 -> " + Thread.currentThread().isInterrupted());
                e.printStackTrace();
            }
        });
        t1.start();
        TimeUnit.MILLISECONDS.sleep(50);
        t1.interrupt();
    }

线程初始中断状态 -> false
抛出异常后线程中断状态 -> false
java.lang.InterruptedException: sleep interrupted
	at java.lang.Thread.sleep(Native Method)
	at org.dromara.soul.admin.config.Test.lambda$main$0(Test.java:11)
	at java.lang.Thread.run(Thread.java:748)
```



## 思考线程池是否要关闭

FixedThreadPool的核心线程不会超时自动关闭，必须在适当的时候调用shutdown来关闭，否则会一直在内存中存在。

CachedThreadPool线程keepAliveTime默认为60s，若忘记关闭且allowCoreThreadTimeOut(true)时，keepAliveTime时间到60s时自动关闭。

finally线程池的关闭可采用TWR语法糖优化Try with Resource

## 线程池关闭后的影响

### 线程池关闭是否可以接受新任务？

默认的handle是 Abort policy，继续提交任务会执行拒绝策略，implements RejectedExecutionHandler可以修改具体拒绝策略。

### 等待队列里的任务是否会继续执行？正在执行 的任务是否会立即中断？

执行shutdown( )，等待队列里的任务会继续执行，全部执行完后真正shutdown。执行shutdown( )和真正shutdown（）shutdown( )之间，会拒绝新任务，调用rejectedExecutionHandler来处理这个任务，默认的rejectedExecutionHandler是AbortPolicy并抛异常。方法不会 interrupt 运行中running线程。

执行shutdownNow( )，线程池里的等待任务不会继续执行。

# 队列

## 线程阻塞的两种情况

（1）队列中没数据，消费端所有线程都自动阻塞挂起直到有数据进入队列。

（2）当生产者填满队列数据时，生产端的所有线程都会被自动阻塞挂起，直到队列有空位置，生产者线程被自动唤醒。

## 阻塞队列BlockingQueue

BlockingQueue内存队列，生产者put，消费者take。当队列为空，消费者线程被阻塞；当队列装满，生产者线程被阻塞。

### demo 花牌游戏 Epam面试手写代码

```java
/**
 * Task1: Please represent 54 playing Card Deck as a Java class. Imagine which methods could be placed inside.
 * Task2: Using task1 as your class. Imagine there are 1 card sender and 3 players. The card sender send card to player one by one in a round. Once the player’s sum points bigger than 50, the player win the game.  
 * [Points define]
 * "A"=1,"2"=2,"3"=3,"4"=4,"5"=5,"6"=6,"7"=7,"8"=8,"9"=9,"10"=10,"J"=11,"Q"=12,"K"=13,"black Joke"=20,"red Joke"=20;
 * Example 1:
 * Round1 = Sender ["A","6","K"=13] -> Player1=1, player2=6, player3=13;
 * Round2 = Sender ["10","Q","black Joke"]-> Player1=11, player2=18, player3=33;
 * Round3 = Sender ["9","J","red Joke"]-> Player1=20, player2=29, player3=53-> player 3 win;
 */
```

牌

```java
public class Card {

    private String name;
    private int point;

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Card card = (Card) o;
        return point == card.point &&
                name.equals(card.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, point);
    }
}
```

牌花色

```java
public enum SuitsEnum {
    SPADES,
    HEARTS,
    DIAMONDS,
    CLUBS
}
```

玩牌者

```java
public class Player {
    private static final int ROUND = 3;

    /**
     * 玩家id
     */
    private int id;
    /**
     * 玩家名
     */
    private String name;
    /**
     * 玩家手里的牌
     */
    private ArrayList<Card> list;

    public Player(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public void getCard(Card card){
        if(CollectionUtils.isEmpty(list)){
            list = new ArrayList<>(ROUND);
        }
        list.add(card);
    }
```

点数 牌A-K 13张

```java
public enum PointsEnum {
    A("A",1),
    _2("2",2),
    _3("3",3),
    _4("4",4),
    _5("5",5),
    _6("6",6),
    _7("7",7),
    _8("8",8),
    _9("9",9),
    _10("10",10),
    J("J",11),
    Q("Q",12),
    K("K",13);

    PointsEnum(String name, int rank) {
        this.name = name;
        this.rank = rank;
    }
    private String name;
    private int rank;
}
```

荷官

```java
public class Sender {
    private static ArrayList<Card> arrayList = new ArrayList<>(54);

    public ArrayList<Card> init() {
        for (SuitsEnum suit : SuitsEnum.values()) {
            for (PointsEnum point : PointsEnum.values()) {
                arrayList.add(new Card(suit.name().toLowerCase() + " " + point.getName(), point.getRank()));
            }
        }
        arrayList.add(new Card("black Joke", 20));
        arrayList.add(new Card("red Joke", 20));
        return arrayList;
    }


    public void shuffle(ArrayList<Card> arrayList) {
        Collections.shuffle(arrayList);
    }
```



```java
public class BlockingQueueTest {
    private static BlockingQueue<Card> cards = new LinkedBlockingDeque<>();

    public static Card take() {
        Card card = null;
        try {
            card = cards.take();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        return card;
    }

    public static void put(Card card) {
        try {
            cards.put(card);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    public static boolean win(Player[] players) {
        if (null != players && 0 != players.length) {
            for (Player player : players) {
                // 每个玩家手中的牌
                ArrayList<Card> list = player.getList();
                if (!CollectionUtils.isEmpty(list)) {
                    System.out.println(MessageFormat.format("{0}-{1}-{2}", player.getId(), player.getName(), JSON.toJSON(player.getList())));
                    int sum = list.stream().mapToInt(c -> c.getPoint()).sum();
                    if (sum > 50) {
                        System.out.printf("%d-%s sum:%d%s%n", player.getId(), player.getName(), sum, JSON.toJSON(player.getList()));
                        return true;
                    }
                }
            }
        }
        return false;
    }


    public static void main(String[] args) {
        // 1个发牌者
        Sender sender = new Sender();
        // 54张牌
        ArrayList<Card> cardList = sender.init();
        // 发牌者洗牌
        sender.shuffle(cardList);

        // 3个玩家
        Player[] players = new Player[3];
        players[0] = new Player(1, "Player1");
        players[1] = new Player(2, "Player2");
        players[2] = new Player(3, "Player3");

        // 游戏共多少轮数
        int rounds = 18;
        for (int j = 0; j < rounds; j++) {
            Iterator<Card> it = cardList.iterator();
            if (it.hasNext()) {
                // 一轮中，顺序发三张
                for (int i = 0; i < 3; i++) {
                    Card currentCard = it.next();
                    // 取一张删掉一张
                    put(currentCard);
                    it.remove();
                }
            }
            players[0].getCard(take());
            players[1].getCard(take());
            players[2].getCard(take());


            System.out.printf("round%d is over%n", j);
            if (win(players)) break;
        }
    }

}
```

### Java API-常用方法

#### 放

```css
offer(anObject): 表示如果可能的话，将an Object加到BlockingQueue里，即如果BlockingQueue可以容纳，
　　　　则返回true，否则返回false。（本方法不阻塞当前执行方法的线程）
offer(E o, long timeout, TimeUnit unit): 可以设定等待的时间，如果在指定的时间内，还不能往队列中
　　　　加入BlockingQueue，则返回失败。
put(anObject): 把an Object加到BlockingQueue里，如果BlockQueue没有空间，则调用此方法线程被阻断
　　　　直到BlockingQueue里面有空间再继续。
```

#### 取

```css
poll(time):取走BlockingQueue里排在首位的对象，若不能立即取出，则可以等time参数规定的时间，
　　　　取不到时返回null；
poll(long timeout, TimeUnit unit)：从BlockingQueue取出一个队首的对象，如果在指定时间内，
　　　　队列一旦有数据可取，则立即返回队列中的数据。否则直到时间超时还没有数据可取，返回失败。
take( ): 取走BlockingQueue里排在首位的对象，若BlockingQueue为空，阻断进入等待状态直到
　　　　BlockingQueue有新的数据被加入。 
drainTo( ): 一次性从BlockingQueue获取所有可用数据对象（还可指定获取数据的个数），不需多次分批加锁或释放锁，提升获取数据效率。
```



## ArrayBlockingQueue（FIFO）

数组结构组成的有界阻塞队列，直接将枚举对象插入或移除，不会产生额外对象实例。默认不保证公平访问队列。

公平访问队列是指阻塞所有生产者线程或消费者线程，当队列可用时，可按照阻塞的先后顺序访问队列，先阻塞的生产者线程可以先往队列里插入元素，先阻塞的消费者线程，可以先从队列里获取元素。添加和移除操作都采用同一把锁ReenterLock( );初始化必须传入容量大小，使用int来统计元素。

## LinkedBlockingQueue（newFixedThreadPool） VS LinkedTransferQueue VS LinkedBlockingDeque

LinkedBlockingQueue线程安全的阻塞队列。链表结构组成的有界阻塞队列，LinkedBlockingQueue中锁分离，插入（添加）是用putLock，移除是用takeLock，好处是大大提高队列的吞吐量，在高并发下生产者和消费者可并行操作队列中的数据来提高整个队列的并发性能。

适合生产和消费频率差不多的场景。大批量数据系统，GC压力大。

默认Integer.MAX_VALUE大小，也可指定容量大小。
clear会加上两把锁，使用AtomicInteger来统计元素的个数。

LinkedTransferQueue链表结构组成的无界阻塞队列。

LinkedBlockingDeque链表结构组成的双向阻塞队列。

## PriorityBlockingQueue

优先级排序的无界阻塞队列

## DelayQueue（缓存失效、定时任务）

优先级队列实现的无界阻塞队列。创建元素可指定多久才能从队列获取当前元素，在延迟期满才能从队列中提取元素。

DelayQueue保存缓存元素的有效期，使用一个线程循环查询DelayQueue，一旦能从DelayQueue中获取元素，表示缓存有效期到了。

## SynchronousQueue（不存储数据、可传递数据）

不存储元素的阻塞队列。每一个put操作必须等待一个take操作，否则不能继续添加元素。

# 线程安全

线程安全指控制多个线程对某个资源的有序访问或修改（一个类在可以被多个线程安全调用时就是线程安全）。

```css
更深刻的描述：
(1)可以从多个编程线程中调用，无需线程之间不必要的交互。
(2)可以同时被多个线程调用，不需要调用一方有任何操作。
```

线程安全实质是公共区域的内存所存数据的安全，一般是堆内存和方法区。方法区存的是（1）类型信息（2）类型的常量池（3）字段信息（4）方法信息（5)类变量（6）指向类加载器的引用（7）指向class实例的引用（8）方法表。注意运行时常量池存在JDK 1.6方法区的 PermGen、JDK 1.7 heap、JDK 1.8 metaspace。

## 有状态 VS 无状态

| 状态            | 是否有实例对象 | 是否可以保存数据 | 线程是否安全 |
| :-------------- | :------------: | :--------------: | :----------: |
| 有状态Stateful  |       是       |        是        |      否      |
| 无状态Stateless |   无，不变类   |        否        |      是      |

## 有条件线程安全



# 线程同步 VS 线程异步

## 同步 VS 异步

同步：当一个线程A对内存操作时其他线程都不对内存地址操作，直到线程A完成操作，其他线程才能对内存地址进行操作，且其他线程处于等待状态。

实质是任一时刻只有一个线程在跑，其他线程处x于等待。

同步是为了协同相互配合，按预定的先后次序进行工作。

## 同步使用场景

一些敏感数据不允许被多个线程同时访问，比如修改、计算

时序就近操作

## 异步使用场景

无时序操作

IO等耗时操作

不影响主线程结果

对共享资源只读、无原子性操作长流程

# Java API-线程同步的方法

```java
java.lang.Thread#sleep(long)
java.lang.Object#wait()
java.lang.Object#notifyAll()
java.lang.Object#notify()
```

# 对象头Mark Word

存放在堆中的对象分为三部分：对象头、实例变量(对象属性信息、包括父类属性信息）、填充字节对齐padding(JVM要求对象字节必须是8个字节的整数倍，用于凑齐整数倍)

```c++
ObjectMonitor() {
    _count        = 0; 		//用来记录该对象被线程获取锁的次数
    _waiters      = 0;
    _recursions   = 0; 		//锁的重入次数
    _owner        = NULL; 	//指向持有ObjectMonitor对象的线程 
    _WaitSet      = NULL; 	//处于wait状态的线程，会被加入到_WaitSet
    _WaitSetLock  = 0 ;
    _EntryList    = NULL ; 	//处于等待锁block状态的线程，会被加入到该列表
}
```

# 64位虚拟机对象头存储

![OS 64bit markword](http://hongchengjian.gitee.io/md/img/jvm/OS%2064bit%20markword.png)

# Java API-多线程同步5种方式

#### synchronized原理图

![synchronized](http://hongchengjian.gitee.io/md/img/thread/synchronized.png)

synchronized可以将++i或i++等运算或一个方法(函数)变成一个原子操作。注意：当一个线程访问object的一个加锁代码块时，另一个线程仍可以访问该object中的非加锁代码块。

单CPU单线程下++、--操作不加同步，线程安全吗？

单CPU多线程下++、--操作不加同步，线程安全吗？ 不安全

多CPU单线程下++、--操作不加同步，线程安全吗？ 不安全

### 1.synchronized(this)

### 2.synchronized method

#### synchronized method == synchronized(this)



##### synchronized(this)  插入monitorenter、monitorexit

```java
public class Sync {
   public int i;
   public void incre(){
       synchronized (this){
           i++;
       }
   }
}
```

class文件到汇编

```shell
javac Sync.java
javap -v Sync.class > Sync.txt
```



```java
Classfile /D:/czt/user-service/src/main/java/org/union/czt/test/Sync.class
  Last modified 2020-8-25; size 400 bytes
  MD5 checksum 305a718f6262336ffeb6c6bddbb72bb6
  Compiled from "Sync.java"
public class org.union.czt.test.Sync
  minor version: 0
  major version: 52
  flags: ACC_PUBLIC, ACC_SUPER
Constant pool:
   #1 = Methodref          #4.#18         // java/lang/Object."<init>":()V
   #2 = Fieldref           #3.#19         // org/union/czt/test/Sync.i:I
   #3 = Class              #20            // org/union/czt/test/Sync
   #4 = Class              #21            // java/lang/Object
   #5 = Utf8               i
   #6 = Utf8               I
   #7 = Utf8               <init>
   #8 = Utf8               ()V
   #9 = Utf8               Code
  #10 = Utf8               LineNumberTable
  #11 = Utf8               incre
  #12 = Utf8               StackMapTable
  #13 = Class              #20            // org/union/czt/test/Sync
  #14 = Class              #21            // java/lang/Object
  #15 = Class              #22            // java/lang/Throwable
  #16 = Utf8               SourceFile
  #17 = Utf8               Sync.java
  #18 = NameAndType        #7:#8          // "<init>":()V
  #19 = NameAndType        #5:#6          // i:I
  #20 = Utf8               org/union/czt/test/Sync
  #21 = Utf8               java/lang/Object
  #22 = Utf8               java/lang/Throwable
{
  public int i;
    descriptor: I
    flags: ACC_PUBLIC

  public org.union.czt.test.Sync();
    descriptor: ()V
    flags: ACC_PUBLIC
    Code:
      stack=1, locals=1, args_size=1
         0: aload_0
         1: invokespecial #1                  // Method java/lang/Object."<init>":()V
         4: return
      LineNumberTable:
        line 3: 0

  public void incre();
    descriptor: ()V
    flags: ACC_PUBLIC
    Code:
      stack=3, locals=3, args_size=1
         0: aload_0
         1: dup
         2: astore_1
         3: monitorenter
         4: aload_0
         5: dup
         6: getfield      #2                  // Field i:I
         9: iconst_1
        10: iadd
        11: putfield      #2                  // Field i:I
        14: aload_1
        15: monitorexit
        16: goto          24
        19: astore_2
        20: aload_1
        21: monitorexit
        22: aload_2
        23: athrow
        24: return
      Exception table:
         from    to  target type
             4    16    19   any
            19    22    19   any
      LineNumberTable:
        line 6: 0
        line 7: 4
        line 8: 14
        line 9: 24
      StackMapTable: number_of_entries = 2
        frame_type = 255 /* full_frame */
          offset_delta = 19
          locals = [ class org/union/czt/test/Sync, class java/lang/Object ]
          stack = [ class java/lang/Throwable ]
        frame_type = 250 /* chop */
          offset_delta = 4
}
SourceFile: "Sync.java"

```

##### synchronized method  flags:  ACC_SYNCHRONIZED，并没有插入monitorenter、monitorexit

```java
package org.union.czt.test;

public class SyncMethod {
    public int i;

    public synchronized void syncTask() {
        i++;
    }
}
```



```shell
javac SyncMethod.java
javap -v SyncMethod.class > SyncMethod.txt
```



```java
Classfile /D:/czt/user-service/src/main/java/org/union/czt/test/SyncMethod.class
  Last modified 2020-8-25; size 303 bytes
  MD5 checksum 51071a590b1d205d4ea19a04851286ff
  Compiled from "SyncMethod.java"
public class org.union.czt.test.SyncMethod
  minor version: 0
  major version: 52
  // ACC_PUBLIC代表public修饰，ACC_SYNCHRONIZED指明该方法为同步方法     
  flags: ACC_PUBLIC, ACC_SUPER
Constant pool:
   #1 = Methodref          #4.#14         // java/lang/Object."<init>":()V
   #2 = Fieldref           #3.#15         // org/union/czt/test/SyncMethod.i:I
   #3 = Class              #16            // org/union/czt/test/SyncMethod
   #4 = Class              #17            // java/lang/Object
   #5 = Utf8               i
   #6 = Utf8               I
   #7 = Utf8               <init>
   #8 = Utf8               ()V
   #9 = Utf8               Code
  #10 = Utf8               LineNumberTable
  #11 = Utf8               syncTask
  #12 = Utf8               SourceFile
  #13 = Utf8               SyncMethod.java
  #14 = NameAndType        #7:#8          // "<init>":()V
  #15 = NameAndType        #5:#6          // i:I
  #16 = Utf8               org/union/czt/test/SyncMethod
  #17 = Utf8               java/lang/Object
{
  public int i;
    descriptor: I
    flags: ACC_PUBLIC

  public org.union.czt.test.SyncMethod();
    descriptor: ()V
    flags: ACC_PUBLIC
    Code:
      stack=1, locals=1, args_size=1
         0: aload_0
         1: invokespecial #1                  // Method java/lang/Object."<init>":()V
         4: return
      LineNumberTable:
        line 3: 0

  public synchronized void syncTask();
    descriptor: ()V
    flags: ACC_PUBLIC, ACC_SYNCHRONIZED
    Code:
      stack=3, locals=1, args_size=1
         0: aload_0
         1: dup
         2: getfield      #2                  // Field i:I
         5: iconst_1
         6: iadd
         7: putfield      #2                  // Field i:I
        10: return
      LineNumberTable:
        line 7: 0
        line 8: 10
}
SourceFile: "SyncMethod.java"

```

#### synchronized static method == synchronized(obj)

```
synchronized static method = synchronized(Object.class) 锁的是class实例，class相关数据存储在（1.6 PermGen、1.7 heap、1.8 metaspace），Object.class信息是共享的，静态方法锁相当于全局锁，会锁住所有调该方法的线程。

ex. Thread t1 = new Thread( );  	t1.start( );
Thread t2 = new Thread( );    		t2.start( );
此种情况下 t1执行了，t2不能执行，因为t2不能进入锁。

https://www.cnblogs.com/GnagWang/archive/2011/02/27/1966606.html#!comments
```

#### synchronized(obj) VS synchronized method 

synchronized(obj)粒度更细，synchronized(obj)更灵活。obj可以是this。synchronized method会将其他不需同步的代码也加上锁，效率稍差些。

### 3.volatile

#### 特点

禁止指令重排序、多线程可见性。 只能保证可见性，不能保证原子性。

#### volatile不保证原子性原因

```
线程之间读取到同样的值然后相互覆盖对方的值 https://blog.csdn.net/weixin_30410999/article/details/98829679
```

#### 多线程可见性

##### Java内存模型

![volatile](http://hongchengjian.gitee.io/md/img/thread/volatile.png)

##### 主内存 VS 工作内存　

主内存：线程共享，方法区和堆

工作内存：线程私有，栈，主内存变量copy的寄存器(包括程序计数器PC和CPU工作的高速缓存)

多个线程之间是不能互相传递数据通信，多线程之间的沟通只能通过共享变量来进行。

##### JVM规范定义线程对内存交互操作8个

```css 
Lock(锁定)：作用于主内存中的变量，把一个变量标识为一条线程独占的状态。
Read(读取)：作用于主内存中的变量，把一个变量的值从主内存传输到线程的工作内存中。
Load(加载)：作用于工作内存中的变量，把read操作从主内存中得到的变量的值放入工作内存的变量副本中。
Use(使用)：作用于工作内存中的变量，把工作内存中一个变量的值传递给执行引擎。
Assign(赋值)：作用于工作内存中的变量，把一个从执行引擎接收到的值赋值给工作内存中的变量。
Store(存储)：作用于工作内存中的变量，把工作内存中的一个变量的值传送到主内存中。
Write(写入)：作用于主内存中的变量，把store操作从工作内存中得到的变量的值放入主内存的变量中。
Unlock(解锁)：作用于主内存中的变量，把一个处于锁定状态的变量释放出来，之后可被其它线程锁定。
```

##### 可见性Copy过程

前提有三个线程1，2，3，假设线程1修改了volatile修饰的变量值，线程2和3可以知道线程1修改后的具体值：

从线程1的工作内存到主内存：Assign(赋值) ---> Store(存储)---> Write(写入)  疑问是开始加Lock锁定？操作结束Unlock解锁？

从主内存到线程2和3的工作内存：Read(读取)---> Load(加载) --->Use(使用)

##### 8个Happen-Before机制

```css
1、单线程happen-before原则：
 在同一个线程中，书写在前面的操作happen-before后面的操作。
2、锁的happen-before原则：
同一个锁的unlock操作happen-before此锁的lock操作。
3、volatile的happen-before原则：
对一个volatile变量的写操作happen-before对此变量的任意操作(当然也包括写操作了)。
4、happen-before的传递性原则：
如果A操作 happen-before B操作，B操作happen-before C操作，那么A操作happen-before C操作。
5、线程启动的happen-before原则：
同一个线程的start方法happen-before此线程的其它方法。
6、线程中断的happen-before原则：
对线程interrupt方法的调用happen-before被中断线程的检测到中断发送的代码。
7、线程终结的happen-before原则：
线程中的所有操作都happen-before线程的终止检测。
8、对象创建的happen-before原则：
一个对象的初始化完成先于他的finalize方法调用。
```



#### volatile使用场景

ConcurrentHashMap多线程的读 get( )没加锁，实现依赖于volatile。

DCL单例必须要volatile

多线程循环中的判断开关是否停止线程

### 4.ReentrantLock

#### ReentrantLock VS synchronized 

ReentrantLock 优点

```css
（1）响应中断：lockInterruptibly( )可以使线程在被阻塞时响应中断
（2）可轮询获取锁: tryLock()调用时锁为空闲状态才获取该锁。如果锁可用，则获取锁，并立即返回值true。如果锁不可用，则此方法将立即返回值false
（3）定时：tryLock(long, TimeUnit)
（4）多Condition：newCondition( ) signal( ) await( )  思考condition作用？
```

synchronized：悲观锁、非公平、可重入、重锁(JDK 1.5)、JDK1.8 synchronized 默认是轻量级锁，锁升级：偏向锁->轻量级锁->重量级锁。

ReentrantLock：非公平锁（默认的lock方法是非公平 默认构造器传boolean类型值）、公平锁、悲观、可重入、互斥锁（独享锁）。

synchronized会被JVM自动解锁，但ReentrantLock加锁后需手动解锁（异常会导致无法正常解锁，finally无论执行过程中是否出现异常，肯定会最终执行）。

#### CAS

CAS注意区分是Compare and Swap还是Compare and Set

（1） Compare and Swap：乐观锁，常见实现数据库乐观锁做version，操作就version+1比较更新。

```css
补充：
    数据库当前时间戳可做乐观锁？
    数据库悲观锁是for update。
    数据库悲观行锁是 where id = XX for update。
```

CAS核心思想是 数据读出来的时候有一个版本v1，在内存中修改，再写回去时发现数据库中的版本不是v1，说明在修改期间别的事务也在修改，则放弃更新操作，把数据重新读出来，重新计算逻辑再重新写回去，不断地重试。

（2）Compare and Set：AtomicXXX

```java
java.util.concurrent.atomic.AtomicLong
//+1操作
public final long getAndIncrement() {
  while (true) {
    long current = get();
    long next = current + 1;
    //当+1操作成功的时候直接返回，退出此循环
    if (compareAndSet(current, next))
      return current;
  }
}

//调用JNI（Java Native Interface）实现CAS
public final boolean compareAndSet(long expect, long update) {
  return unsafe.compareAndSwapLong(this, valueOffset, expect, update);
}
```

#### AQS

AQS：先CAS乐观，后悲观（LCH双向链表修改state做判断）。

阻塞其他线程 VS 不阻塞其他线程

当前加锁对象同一个对象释放锁 VS 其他对象释放锁

先加锁先释放锁 VS 允许插队后直接释放锁

### 5. ThreadLocal

底层是ThreadLocalMap存线程副本。每个Thread都对应一个ThreadLocalMap。数据是以线程为作用域并且不同线程具有不同的数据副本时，采用ThreadLocal。

#### threadLocal为什么用它？

解决多个线程变量冲突。线程隔离每个线程的私有变量。解决跨函数（方法）的共享变量问题。方法间传递的共享变量。跨的是一个线程贯穿的所有函数（方法）。从变量角度来看ThreadLocal，ThreadLocal类似上下文，一般使用时要private static final ThreadLocal<Context> LOCAL = new ThreadLocal<Context>( )，Context支持变量的种类更丰富（因map的value可以是任何类型，map的key可以为null，key为null时，hashcode是0，是数组的第一个元素）。

#### ThreadLocal主要方法

get( )、set( )、remove( )、initialValue( )

其中initialValue( )是延迟调用，protected是让子类覆写，在线程第1次调用get()或set(Object)时才执行，并且仅执行1次。

```java
public class ThreadLocal<T> {    
	/**
     * Returns the value in the current thread's copy of this
     * thread-local variable.  If the variable has no value for the
     * current thread, it is first initialized to the value returned
     * by an invocation of the {@link #initialValue} method.
     *
     * @return the current thread's value of this thread-local
     */
    public T get() {
        Thread t = Thread.currentThread();
        ThreadLocalMap map = getMap(t);
        if (map != null) {
            // ThreadLocalMap的key是当前ThreadLocal对象
            ThreadLocalMap.Entry e = map.getEntry(this);
            if (e != null) {
                @SuppressWarnings("unchecked")
                T result = (T)e.value;
                return result;
            }
        }
        return setInitialValue();
    }
}
```



```java
public class Thread implements Runnable {
	
	/* ThreadLocal values pertaining to this thread. This map is maintained
     * by the ThreadLocal class. */
    ThreadLocal.ThreadLocalMap threadLocals = null;
   
	/**
     * Get the map associated with a ThreadLocal. Overridden in
     * InheritableThreadLocal.
     *
     * @param  t the current thread
     * @return the map
     */
    ThreadLocalMap getMap(Thread t) {
        return t.threadLocals;
    }
}

```



#### 为什么是弱引用？而不是强引用？

弱引用不稳定，很容易被回收，一旦被回收，其登记的key-value形式的数据，此时就变成了null-value，key都消失了，value就找不到了，造成内存泄漏。弱引用只能存活到下一次垃圾收集之前。本质是一个map，集合肯定不是无限制存数据的，集合有上限大小限制。

```java
WeakReference<String> weakReference = new WeakReference<String>(new String("www.threadlocal.cn"));

System.gc();// 强制一次gc()
// 测试一次弱引用的生命周期
if(weakReference.get() == null)
{
    System.out.println("weakReference已经被GC回收");
}

```

threadLocal存的是线程私有变量还是线程公共变量？线程私有变量。

#### 为什么不用new，用threadlocal？

多个线程进来是要排队，排队只能某个时刻服务一个线程。用threadLocal是为每一个线程都对应提供一个自己的空间map，多个线程可以同时访问。

threadLocal存的是方法间的共享变量还是线程之间的共享变量？方法间。

threadLocal是线程间共享？不是。

方法method1(args) 、method2(args)… methodN(args) 若是都要用到这个args作业务逻辑处理，则每个方法都需要创建args在方法链上往后依次传入。而用threadLocal方便直接取，减少了多次创建args的性能损耗

#### ThreadLocal使用上问题

static final 修饰贯穿整个线程的生命周期

线程执行完成后ThreadLocal.remove( )

TLA：java.lang.OutOfMemoryError: getNewTla.

ThreadLocalArea大小值 -[XXtlaSize:min=16k,preferred=](http://docs.oracle.com/cd/E13150_01/jrockit_jvm/jrockit/jrdocs/refman/optionXX.html#wp1020097)1024k,wasteLimit=16k

-XXlargeObjectLimit，限制在本地线程创建对象的最大值

#### demo

```java
// 为每个线程都会开一个连接
private static ThreadLocal<Connection> connectionHolder
    = new ThreadLocal<Connection>() {
    public Connection initialValue() {
        return DriverManager.getConnection(DB_URL);
    }
};
 
public static Connection getConnection() {
    return connectionHolder.get();
}

```

### InheritableThreadLocal 实现父线程到子线程的值传递原理

```java
public class Thread implements Runnable {
    
    /* ThreadLocal values pertaining to this thread. This map is maintained
     * by the ThreadLocal class. */
    ThreadLocal.ThreadLocalMap threadLocals = null;

    /*
     * InheritableThreadLocal values pertaining to this thread. This map is
     * maintained by the InheritableThreadLocal class.
     */
    ThreadLocal.ThreadLocalMap inheritableThreadLocals = null;
    
    
	private void init(ThreadGroup g, Runnable target, String name,long stackSize, 				                                AccessControlContext acc, boolean inheritThreadLocals) {
                      
        // ...
        // 传递时机在创建Thread时。在线程池复用情景中，并没有创建Thread的触发机制，阿里TransmittableThreadLocal解决
        if (inheritThreadLocals && parent.inheritableThreadLocals != null)
            this.inheritableThreadLocals =
            ThreadLocal.createInheritedMap(parent.inheritableThreadLocals);
        // ...
                      
	}
}

```



```java
public class ThreadLocal<T> {
    
	static ThreadLocalMap createInheritedMap(ThreadLocalMap parentMap) {
        return new ThreadLocalMap(parentMap);
    }

    /**
     * Construct a new map including all Inheritable ThreadLocals
     * from given parent map. Called only by createInheritedMap.
     *
     * @param parentMap the map associated with parent thread.
     */
    private ThreadLocalMap(ThreadLocalMap parentMap) {
        Entry[] parentTable = parentMap.table;
        int len = parentTable.length;
        setThreshold(len);
        table = new Entry[len];

        for (int j = 0; j < len; j++) {
            Entry e = parentTable[j];
            if (e != null) {
                @SuppressWarnings("unchecked")
                ThreadLocal<Object> key = (ThreadLocal<Object>) e.get();
                if (key != null) {
                    Object value = key.childValue(e.value);
                    Entry c = new Entry(key, value);
                    int h = key.threadLocalHashCode & (len - 1);
                    while (table[h] != null)
                        h = nextIndex(h, len);
                    table[h] = c;
                    size++;
                }
            }
        }
    }
}
    
    

```



InheritableThreadLocal中createMap，以及getMap方法处理的对象不一样。其中在ThreadLocal中处理的是threadLocals，而InheritableThreadLocal中处理的是inheritableThreadLocals
    
当父线程对inheritableThreadLocals赋值，就会将父线程的inheritableThreadLocals执行createInheritedMap方法(这个方法就是将线程的threadLocalMap传递给子线程)

### 调用链跨线程传递ThreadLocal

```java
在Tracing框架中，Trace信息传递基于ThreadLocal，

ThreadLocal<String> traceContext = new ThreadLocal<>();
 
String traceId = Tracer.startServer();
// 生成trace信息 传入threadlocal
traceContext.set(traceId);
...
// 从threadlocal获取trace信息
Tracer.startClient(traceContext.get()); 
Tracer.endClient();
...
// 异步线程，下一个Span拿不到上一个Span的trace信息，调用链跟踪断了


```

### 阿里TransmittableThreadLocal原理（对于框架来说，性能并不优越，不建议采用，对于业务系统性能损耗可以接受）

```java
public class TransmittableThreadLocal<T> extends InheritableThreadLocal<T> {
 	// holder是一个InheritableThreadLocal变量，该变量在子线程执行过程中(TtlExecutors提供了在子线程执行时加入复制父线程的ThreadLocal)，缓存了所有线程TransmittableThreadLocal(父线程+子线程)
    static InheritableThreadLocal<Map<TransmittableThreadLocal<?>, ?>> holder = new InheritableThreadLocal<Map<TransmittableThreadLocal<?>, ?>>() {
        protected Map<TransmittableThreadLocal<?>, ?> initialValue() {
            return new WeakHashMap();
        }
 
        protected Map<TransmittableThreadLocal<?>, ?> childValue(Map<TransmittableThreadLocal<?>, ?> parentValue) {
            return new WeakHashMap(parentValue);
        }
    };
    // set缓存父线程
    public final void set(T value) {
        super.set(value);
        // 提供set null移除value的功能
        if (null == value) {
            this.removeValue();
        } else {
            this.addValue();
        }
 
    }
 	// get缓存子线程
    public final T get() {
        T value = super.get();
        if (null != value) {
            this.addValue();
        }
 
        return value;
    }
 
    void addValue() {
        if (!((Map)holder.get()).containsKey(this)) {
            ((Map)holder.get()).put(this, (Object)null);
        }
    }
 
}
```

### TtlExecutors类使用及源码分析

```java
使用场景
ExecutorService threadPool= TtlExecutors.getTtlExecutorService(Executors.newFixedThreadPool(poolSize));
```

### 阿里TransmittableThreadLocal性能缺陷

```java
框架系统引入会损耗性能，业务系统可选择性引入，性能损耗的原因是？

```

### 框架使用Java Agent植入修饰代码

```

```



# 线程切换

操作系统实现线程之间的切换就是需从用户态切换到核心态。

## 什么是用户态？什么是核心态？

用户态：用户态没能力直接操作硬件，没能力访问任意内存地址，不能执行一些 CPU 特权指令。

核心态：可直接操作外设、硬件。

如Kafka 0-Copy 减少了哪两次copy？

Direct Memory Access DMA直接内存读取

## 上下文

上下文是指某一时间点CPU寄存器和程序计数器的内容。

## 上下文切换 Context Switch

上下文切换实际是CPU寄存器切换。上下文切换基本原理是当发生任务切换时，保存当前任务的寄存器到内存中，将下一个即将要切换过来的任务的寄存器状态恢复到当前CPU寄存器中，使其继续执行，同一时刻只允许一个任务独享寄存器。

上下文切换的信息会一直被保存在CPU的内存中，直到被再次使用。

跨核上下文切换 Cross-Core Context Switch：一个线程可以在多个处理器跨核运行。跨核上下文切换代价高，在另一个处理器内核抢占和调度线程会引起缓存丢失，作为缓存丢失和过度上下文切换的结果要访问本地内存。

单核上下文切换：一个线程在单核处理器运行。

## 上下文切换发生场景

1.当前正在执行的任务完成了，系统CPU正常调度下一个任务。

2.当前正在执行的任务遇到I/O等阻塞操作，调度器挂起任务，继续调度下一个任务。

3.多个任务并发抢占锁资源，当前任务没有抢到锁资源，被调度器挂起，继续调度下一个任务。

4.挂起当前任务，比如sleep( )调用让出CPU

5.硬件中断

## 自愿上下文切换cswch  VS 非自愿上下文切换nvcswch

```css
自愿上下文切换		 voluntary context switches  			指进程无法获取所需资源，导致的上下文切换。比如I/O、内存等系统资源不足

非自愿上下文切换	non voluntary context switches		进程由于时间片已到等原因，被系统强制调度，进而发生的上下文切换。比如说，大量进程都在争抢 CPU 时

```

## Linux查看系统上下文切换

vmstat只给出系统总体上下文切换情况

```shell
FIELD DESCRIPTION FOR VM MODE
   Procs
       r: The number of runnable processes (running or waiting for run time).
       b: The number of processes in uninterruptible sleep.

   Memory
       swpd: the amount of virtual memory used.
       free: the amount of idle memory.
       buff: the amount of memory used as buffers.
       cache: the amount of memory used as cache.
       inact: the amount of inactive memory.  (-a option)
       active: the amount of active memory.  (-a option)

   Swap
       si: Amount of memory swapped in from disk (/s).
       so: Amount of memory swapped to disk (/s).

   IO
       bi: Blocks received from a block device (blocks/s).
       bo: Blocks sent to a block device (blocks/s).

   System
       in: The number of interrupts per second, including the clock.
       cs: The number of context switches per second.

   CPU
       These are percentages of total CPU time.
       us: Time spent running non-kernel code.  (user time, including nice time)
       sy: Time spent running kernel code.  (system time)
       id: Time spent idle.  Prior to Linux 2.5.41, this includes IO-wait time.
       wa: Time spent waiting for IO.  Prior to Linux 2.5.41, included in idle.
       st: Time stolen from a virtual machine.  Prior to Linux 2.6.11, unknown.
```



```shell
[root@xx]# vmstat
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   	buff    cache     si   so    bi    bo   in   cs us sy id wa st
 1  0 1388188 957744      0 	516680    0    0     2     8    0    1  0  0 100  0  0
You have new mail in /var/spool/mail/root

r Running or Runnable 	就绪队列的长度，也就是正在运行和等待CPU的进程数
cs context switch 	    每秒上下文切换次数
in	interrupt		   每秒中断的次数
b	Blocked			   处于不可中断睡眠状态的进程数

```

## Linux查看某个进程详细情况

```shell
pidstat -w pid

-u：默认的参数，显示各个进程的cpu使用统计
-r：显示各个进程的内存使用统计
-d：显示各个进程的IO使用情况
-p：指定进程号
-w：显示每个进程的上下文切换情况
-t：显示选择任务的线程的统计信息外的额外信息
-T { TASK | CHILD | ALL }
这个选项指定了pidstat监控的。TASK表示报告独立的task，CHILD关键字表示报告进程下所有线程统计信息。ALL表示报告独立的task和task下面的所有线程。
注意：task和子线程的全局的统计信息和pidstat选项无关。这些统计信息不会对应到当前的统计间隔，这些统计信息只有在子线程kill或者完成的时候才会被收集。
-V：版本号
-h：在一行上显示了所有活动，这样其他程序可以容易解析。
-I：在SMP环境，表示任务的CPU使用率/内核数量
-l：显示命令名和所有参数


```

# 多线程

多线程指两个线程的代码可以同时运行，而不必一个线程需要等待另一个线程内的代码执行完才可以运行。对于单核CPU来说，是无法做到真正的多线程的，每个时间点上，CPU都会执行特定的代码，由于CPU执行代码时间很快，所以两个线程的代码交替执行看起来像是同时执行的一样。那具体执行某段代码多少时间，和分时机制系统有关。

分时系统把CPU时间划分为多个时间片Slice，操作系统以时间片为单位片为单位各个线程的代码，越好的CPU分出的时间片越小。 注意多线程debug时，一个任务执行时间<时间片时间，可能一个线程时间片里跑完了所有任务，并没有经过CPU时间片切换再跑其他线程。

## 多线程效果

用多线程不一定比单线程块

T1 创建线程时间，T2 在线程中执行任务的时间，T3 销毁线程时间。T1 + T3 远大于 T2可采用线程池，以提高服务器性能。

### 多线程计数器

AtomicInteger 编写一个线程安全的计数器，5个线程同时跑，计数到1000，输出线程名和计数直到1000 

CountDownLatch  减计数

CyclicBarrier 加计数

|                     CountDownLatch                     |                     CyclicBarrier                      |
| :----------------------------------------------------: | :----------------------------------------------------: |
|                         减计数                         |                         加计数                         |
|               计数为0时释放所有等待线程                |            计数达到指定值时释放所有等待线程            |
|                  计数为0时，无法重置                   |           计数达到指定值，计数置为0重新开始            |
| countDown( )计数减一，await( )只进行阻塞，对计数没影响 | await( )计数加1，若加1后值不等于构造方法值，则线程阻塞 |
|                      不可重复利用                      |                       可重复利用                       |
|            所有线程任务都执行完才进行下一步            |                  信号发出同一时刻运行                  |



### 所有线程任务都执行完才进行下一步

CountDownLatch来计任务数，计数器的初始化大小和任务数的大小一致(注意与线程数无关)，每执行一次任务，计数器countDown减一，await( )一直阻塞主线程，直到计数器值为0，释放锁(所有任务完成才释放)

### 多线程数量不超过CPU核数

# 死锁

## OS-死锁条件

```css
（1） 互斥条件：一个共享资源（临界资源）每次只能被一个进程使用。
（2） 请求与保持（占有且等待）：一个进程因请求资源而阻塞时，对已获得的资源保持不放。P1占有一个资源a，并等待另一个资源b，而该资源a被其他进程占有所以P1阻塞，但P1不释放已获得的资源a。
（3）不可强行占有（不可剥夺（非抢占)):进程已获得的资源，在末使用完之前，不能被其他进程强行剥夺。资源被P1使用，P1使用过程中不能被P2抢占使用，必须等P1使用完自愿释放。
（4） 循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。有一组等待进程 {P0，P1，…，Pn}，P0 等待的资源为 P1 占有，P1 等待的资源为 P2 占有，……，Pn-1 等待的资源为 Pn 占有，Pn 等待的资源为 P0 占有。
只要系统发生死锁，这些条件必然成立，而只要上述条件之一不满足，就不会发生死锁。

```

## 理论-死锁解决方案

思路：可从破坏条件开始

### 死锁预防(严格破坏OS-死锁条件四个条件之一)

有很大可能导致系统资源利用率和系统吞吐量降低

### 死锁避免(死锁避免比死锁预防允许更多的并发)

允许前三个必要条件，但通过算法，确保永远不会到达死锁点

### 死锁避免算法

#### 进程启动拒绝

如果一个进程的请求会导致死锁，则不启动该进程

#### 资源分配拒绝(银行家算法)

**银行家算法**：如果一个进程增加的资源请求会导致死锁，则不允许此分配

### 死锁检测

允许系统在运行过程发生死锁，但可通过系统设置的检测机构及时检测出死锁的发生，并精确地确定于死锁相关的进程和资源，然后采取适当的措施，从系统中将已发生的死锁清除掉。

死锁解除(剥夺资源和撤销进程)

当检测到系统中已发生死锁，需将进程从死锁状态中解脱出来。常用方法：撤销或挂起一些进程，以便回收一些资源，再将这些资源分配给已处于阻塞状态的进程。死锁检测盒解除有可能使系统获得较好的资源利用率和吞吐量，但在实现上难度也最大。

# 锁

## 乐观锁 VS 悲观锁

读多写少 VS 读少写多 思考的重点是阻塞，不阻塞更多的线程。

乐观锁：适合读多写少。Ex.Semaphone、CountDownLatch、ReadWriteLock读锁、CAS、数据库Version。注意带状态、Version的更新必须带上一个Version条件的状态。

悲观锁：适合读少写多。EX. synchronized、ReentrantLock、ReadWriteLock写锁。若写多用乐观锁，大量写每个都CAS会造成大面积阻塞和竞争。

## 公平锁 VS 非公平锁

公平锁（Fair）：考虑排队的线程 FCFS（先对锁提出获取请求的线程先被分配到锁）。

非公平锁（Nonfair）：插队尝试（JVM尝试随机或就近两种分配锁，ReentrantLock默认是非公平锁），不让插队就老实去队尾排队。

非公平锁的性能高于公平锁5～10倍，因为公平锁需在多核CPU情况下维护一个队列。

```java
Lock lock=new ReentrantLock(true);//公平锁 
Lock lock=new ReentrantLock(false);//非公平锁 默认

```

## 可重入锁 VS 非可重入锁

可重入锁（递归锁）：同一线程外层锁、内层还可以加锁或获取锁，嵌套形式。

## 独享锁(互斥锁，独占锁，写锁， 排它锁EXCLUSIVE，一般是悲观锁) VS 共享锁SHARED(读锁，一般是乐观锁)

独享锁（互斥锁，一般是悲观锁，若某个只读线程获取了锁，则其他线程只能等待。避免了读读冲突，但读操作不影响一致性，限制了并发）：同时只能有一个线程获得锁。Ex. ReentrantLock是互斥锁，ReadWriteLock写锁是互斥锁。写锁是代码修改数据，只能一个线程写，且不能同时读，重点是只能一个线程写。

共享锁（读锁，一般是乐观锁，允许多个读操作线程同时访问共享资源）：可以多个线程可同时获得锁。Ex.Semaphone、CountDownLatch是共享锁，ReadWriteLock读锁是共享锁。读锁是代码只读数据，可以很多线程读，但不能同时写，重点是很多线程读。

## 读写锁

如何设计一个读写锁？

![ReadWriteLock](http://hongchengjian.gitee.io/md/img/juc/ReadWriteLock.png)

```java
    	/*
         * Read vs write count extraction constants and functions.
         * Lock state is logically divided into two unsigned shorts:
         * The lower one representing the exclusive (writer) lock hold count,
         * and the upper the shared (reader) hold count.
         */

        static final int SHARED_SHIFT   = 16;
        static final int SHARED_UNIT    = (1 << SHARED_SHIFT);	
 		// (1 << 16)-1 左移16位减1 == 2的16次方-1
		// <<表示二进制左移，即将该数字在二进制下每一位向左移n个，右面补零，数值上扩大了2^n倍
        static final int MAX_COUNT      = (1 << SHARED_SHIFT) - 1;
        static final int EXCLUSIVE_MASK = (1 << SHARED_SHIFT) - 1;
```

ReentrantReadWriteLock中将AQS中的int(32位)类型的state分为高16位与第16位分别记录读锁和写锁的状态。 state&((1<<16)-1)，&是与门，将state的高16位全部抹去，因此state的低位记录着写锁的重入计数。state>>>16 进行无符号补0，右移16位，state的高位记录着写锁的重入计数。

ReentrantReadWriteLock一把读锁ReadLock，一把写锁WriteLock。ReentrantReadWriteLock读写锁互斥，写锁独占，读锁共享，读读不互斥、读写互斥、写写互斥。

读写锁适用场景，高并发情况下，读的操作远远高于写的操作，非高并发下，读写锁由于要额外维护读锁状态，效率不一定比独占锁高。读操作远高于写操作，若不用读写锁，用其他锁会导致读读互斥，高并发下阻塞的线程多。



## 分段锁Segment

分段锁：JDK 1.7 ConcurrentHashMap分16段，最多同时支持16个线程的并发操作。

JDK 1.7 ConcurrentHashMap 数据结构图：

![ConcurrentHashMap分段锁结构](http://hongchengjian.gitee.io/md/img/collection/JDK1.7%20ConcurrentHashMap%20Segment.png)

为什么ConcurrentHashMap后续把分段锁去掉了？JDK 1.7 ConcurrentHashMap是分段锁，JDK 1.8 ConcurrentHashMap降低锁的粒度 。

```css
1.7：Segment + HashEntry + Unsafe
1.8: 移除Segment，使锁的粒度更小，Synchronized + CAS + Node + Unsafe
put( )
    1.7：先定位Segment，再定位bucket，put全程加锁，没有获取锁的线程提前找bucket，并最多自旋64次获取锁，超过则挂起。
    1.8：由于移除了Segment，类似HashMap，可以直接定位到bucket，拿到first节点后进行判断，1、为空则CAS插入；2、为-1则说明在扩容，则跟着一起扩容；3、else则加锁put（类似1.7）
get( ) 
	并发读是依赖volatile, JDK 1.7和JDK1.8都差不多。
resize( )
    1.7：跟HashMap一样，只不过是搬到单线程中执行，避免了HashMap在1.7中扩容时死循环，保证线程安全。
    1.8：支持并发扩容，HashMap扩容在1.8中由头插改为尾插（为了避免死循环问题），ConcurrentHashmap也是，迁移也是从尾部开始，扩容前在bucket的头部放置一个hash值为-1的节点，别的线程访问时就能判断是否该bucket已经被其他线程处理过了。
size( )
    1.7：计算两次，如果不变(调size( )方法计算期间，无新元素插入)则返回计算结果，若不一致，则锁住所有的Segment求和。
    1.8：用baseCount来存储当前的节点个数


```

AtomicXXX：当大量线程同时去访问时，会因为大量线程执行CAS操作失败而进行空转，导致CPU资源消耗过多，而且执行效率也不高。Doug Lea JDK1.8中对CAS进行了优化，基于了CAS分段锁提供了LongAdder。

![LongAdder](http://hongchengjian.gitee.io/md/img/juc/LongAdder.png)

LongAdder父类Striped64维护Cell[]和long base，当多个线程操作一个变量，会先base上进行cas，线程增多时，就使用cell数组。当base将更新值时（调casBase更新base值失败），会自动使用cell数组，每一个线程对应一个cell，每一个线程对cell进行cas操作，可将单一value的更新压力分担到多个value中，大量线程得以分散并发压力，减少了大量线程CAS操作失败而进行空转，提高了并发效率。

## 自旋锁

自旋锁：让线程自旋等一等避免切用户态、核心态的耗时和CPU浪费。

### Q：自旋怎么实现？

```css
wait、notify是条件变量的一种，并不是OS层的自旋，自旋应该是一个空loop，当loop的条件被其他线程改变时再进入临界区，若觉得空循环耗CPU，加上Thread.yield()使线程running ---> runable

```

自旋的实现思想：当一个线程尝试获取某个锁时，如果该锁已被其他线程占用，就一直循环检测锁是否被释放，而不是进入线程挂起或睡眠状态。

自旋锁适用于锁保护的临界区很小的情况，临界区很小的话，锁占用的时间就很短。

https://www.jianshu.com/p/824b2e4f1eed 几种实现

## 偏向锁

### 为什么要偏向锁？

偏向锁：某个线程获得锁之后，消除这个线程以后获取锁重入CAS开销。

轻量级锁（获取及释放锁依赖多次CAS原子指令集）为了在线程交替执行同步块时提高性能，而偏向锁（在置换ThreadID时依赖一次CAS原子指令）在只有一个线程执行同步块时进一步提高性能，因为一个线程多次获得同一个锁不存在锁的竞争。若不用偏向，每次都要竞争锁会增大很多没有必要付出的代价。

### JVM偏向锁相关命令

```shell
-XX:-UseBiasedLocking = false 关闭偏向锁
偏向锁是默认开启的

偏向锁开始时间一般是比应用程序启动慢几秒，不想有这个延迟，命令
-XX:BiasedLockingStartUpDelay=0在对一个Object做syncronized的时候，会立即上一把偏向锁。当处于偏向锁状态时，markword会记录当前线程ID

```

# 锁优化

## 锁膨胀(锁升级)(锁晋升)

### 64 Bit MarkWord

![OS 64bit markword.png](http://hongchengjian.gitee.io/md/img/jvm/OS%2064bit%20markword.png)

锁可以从偏向锁(一次CAS)升级到轻量级锁(获取及释放锁依赖多次CAS原子指令集)，再升级到重量级锁。

### 锁升级路线(单向)

 偏向锁状态---> 轻量级锁状态--->重量级锁状态

![synchronized](http://hongchengjian.gitee.io/md/img/thread/synchronized.png)

### 为什么引入轻量级锁？

轻量级锁考虑的是竞争锁对象的线程不多，线程持有锁的时间也不长的情景。因为阻塞线程需要CPU从用户态转到内核态，如果刚刚阻塞不久这个锁就被释放了，代价较大。干脆不阻塞这个线程，让它自旋这等待锁释放。

### 偏向锁升级轻量级锁

当线程1访问代码块并获取锁对象时，会在java对象头和栈帧中记录偏向的锁的threadID，因为**偏向锁不会主动释放锁**，因此以后线程1再次获取锁的时候，需要**比较当前线程的threadID和Java对象头中的threadID是否一致**，如果一致（还是线程1获取锁对象），则无需使用CAS来加锁、解锁；

偏向锁竞争开始：

如果不一致（其他线程，如线程2要竞争锁对象，而偏向锁不会主动释放因此还是存储的线程1的threadID），需要**查看Java对象头中记录的线程1是否存活**，如果没有存活，那么锁对象被重置为无锁状态，其它线程（线程2）可以竞争将其设置为偏向锁；如果存活，那么立刻**查找该线程（线程1）的栈帧信息LockRecord(LR)，如果还是需要继续持有这个锁对象**，那么暂停当前线程1，撤销偏向锁，升级为轻量级锁，如果线程1 不再使用该锁对象，那么将锁对象状态设为无锁状态，重新偏向新的线程。

其中每个线程通过CAS(自旋)的操作将锁对象头中的markwork设置为指向自己的LR的指针，哪个线程设置成功，就意味着获得锁。

```java
备注：
	与https://yqh.aliyun.com/detail/6169?utm_content=g_1000104857 在偏向锁竞争开始产生观点分歧

```

### 轻量级锁升级重量级锁

线程1获取轻量级锁时会先把锁对象的**对象头MarkWord复制一份到线程1的栈帧中创建的用于存储锁记录的空间**（称为DisplacedMarkWord），然后**使用CAS把对象头中的内容替换为线程1存储的锁记录（**DisplacedMarkWord**）的地址**；

如果在线程1复制对象头的同时（在线程1CAS之前），线程2也准备获取锁，复制了对象头到线程2的锁记录空间中，但是在线程2CAS的时候，发现线程1已经把对象头换了，**线程2的CAS失败，那么线程2就尝试使用自旋锁来等待线程1释放锁**。

但是如果自旋的时间太长也不行，因为自旋是要消耗CPU的，因此自旋的次数是有限制的，比如10次或者100次，如果**自旋次数到了线程1还没有释放锁，或者线程1还在执行，线程2还在自旋等待，这时又有一个线程3过来竞争这个锁对象，那么这个时候轻量级锁就会膨胀为重量级锁。重量级锁把除了拥有锁的线程都阻塞，防止CPU空转。**

### 重量级锁 VS 轻量级锁

重量级锁（Mutex Lock）Ex. Synchronized通过对象内部的监视器锁monitor实现，监视器锁本质是依赖于底层OS的Mutex Lock实现。JDK 1.6以后做了锁膨胀优化：从偏向锁(一次CAS)升级到轻量级锁(获取及释放锁依赖多次CAS原子指令集)，再升级到重量级锁。

### 重量级锁重在哪里？

需做内核态到用户态的转换消耗较多时间

### 偏向锁 VS 轻量级锁  VS 重量级锁

|  锁状态  |                             优点                             |                    缺点                     |                   适用场景                   |
| :------: | :----------------------------------------------------------: | :-----------------------------------------: | :------------------------------------------: |
|  偏向锁  | 加锁无需额外消耗(单线程仅第一次加锁需CAS)和非同步方法时间相差纳秒级 |     竞争的线程多，会有额外的锁撤销消耗      |    基本没有线程竞争锁的同步场景（单线程）    |
| 轻量级锁 |              竞争线程不会阻塞，自旋提高响应速度              | 若一直不能获得锁，长时间的自旋会造成CPU消耗 | 少量线程竞争锁，且锁持有时间短，追求响应速度 |
| 重量级锁 |      线程竞争不适用CPU自旋，不会导致CPU空转消耗CPU资源       |            线程阻塞，响应时间长             |  很多线程竞争锁，锁持有的时间长，追求吞吐量  |

#### 响应速度 VS 吞吐量

响应速度：对请求做出响应的时间快慢

吞吐量：在单位时间内处理请求的数量

### 锁可以升级不可以降级

为了避免无用的自旋，轻量级锁一旦膨胀为重量级锁就不会再降级为轻量级锁了；偏向锁升级为轻量级锁也不能再降级为偏向锁。但是偏向锁状态可以被重置为无锁状态。

### JDK 1.6 synchronized是重量级锁

### JDK1.8 synchronized 默认是轻量级锁，锁升级：偏向锁->轻量级锁->重量级锁

## 减少锁持有时间

只在有需线程安全的程序上加锁

```java
public final class Pattern implements java.io.Serializable {
    public Matcher matcher(CharSequence input) {
        if (!compiled) {
            synchronized(this) {
                if (!compiled)
                    compile();
            }
        }
        Matcher m = new Matcher(this, input);
        return m;
    }
}

```



## 减少锁粒度

大对象进行分片细化成小对象，典型Ex.  JDK1. 7 ConcurrentHashMap 锁细化

## 锁消除 > JDK 1.5

编译器级别。锁消除是指虚拟机即时编译器JIT在运行时，对一些代码上要求同步，对检测到不可能存在共享数据竞争的锁进行削除。

锁消除主要判定依据来源于逃逸分析的数据支持，如果判断到一段代码中，在堆上的所有数据都不会逃逸出去被其他线程访问到，就可以把它们当作栈上数据对待，认为它们是线程私有的，同步加锁自然就无须进行。

```java
 public final class StringBuffer extends AbstractStringBuilder implements java.io.Serializable, CharSequence
{
 	@Override
    public synchronized StringBuffer append(String str) {
        toStringCache = null;
        super.append(str);
        return this;
    }
}

```



```java
public class TestEliminateLocks {
    public static void main(String[] args) {
        long start = System.currentTimeMillis();
        int size = 10000;
        for (int i = 0; i < size; i++) {
            concatStr("hello", "world");
        }
        long timeCost = System.currentTimeMillis() - start;
        System.out.println("concatStr:" + timeCost + " ms");
    }

    // sb仅在concatStr(str1, str2)作用域中有效，不同线程同时调concatStr(str1, str2)都会创建不同的sb对象，若此时append使用同步浪费系统资源
    public static String concatStr(String str1, String str2) {
        StringBuffer sb = new StringBuffer();
        // append方法是同步操作
        sb.append(str1);
        sb.append(str2);
        return sb.toString();
    }
}
```



```shell
-server -XX:+DoEscapeAnalysis -XX:+EliminateLocks 
+DoEscapeAnalysis表示开启逃逸分析，+EliminateLocks表示锁消除
```



```java
This is an example of manual "lock coarsening" and may have been done to get a performance boost.

Consider these two snippets:
// the first case
StringBuffer b = new StringBuffer();
for(int i = 0 ; i < 100; i++){
    b.append(i);
}
versus:
// the second case
StringBuffer b = new StringBuffer();
synchronized(b){
  for(int i = 0 ; i < 100; i++){
     b.append(i);
  }
}
In the first case, the StringBuffer must acquire and release a lock 100 times (because append is a synchronized method), whereas in the second case, the lock is acquired and released only once. This can give you a performance boost and is probably why the author did it. In some cases, the compiler can perform this lock coarsening for you (but not around looping constructs because you could end up holding a lock for long periods of time).

By the way, the compiler can detect that an object is not "escaping" from a method and so remove acquiring and releasing locks on the object altogether (lock elision) since no other thread can access the object anyway. A lot of work has been done on this in JDK7.
```



## 锁粗化

对同一个锁不停地进行请求、同步和释放，本身也会消耗系统宝贵的资源，不利于性能的优化。锁的请求、同步与释放本身会带来性能损耗，高频的锁请求不利于系统性能。**把很多次锁的请求合并成一个请求，以降低短时间内大量锁请求、同步、释放的性能损耗**

```java
public void doSth(){
    synchronized(lock){
        //do some thing
    }
    // logic代码，做其它不需要同步的工作，但能很快执行完毕
    synchronized(lock){
        //do other thing
    }
}

```

前提是中间不需要同步的代码能够很快速地完成

```java
public void doSomethingMethod(){
    // 进行锁粗化：整合成一次锁请求、同步、释放
    synchronized(lock){
        //do some thing
        // logic代码，做其它不需要同步的工作，但能很快执行完毕
        //do other thing
    }
}

```



## 锁分离

ReadWriteLock读锁、写锁分离，实现读读不互斥、读写互斥、写写互斥。LinkedBlockingQueue从头部取出，从尾部放数据。

## 锁续约

分布式锁redisson 锁过期expire时间比执行完任务时间要长，redisson(加锁、解锁、续约)看门狗WatchDog在加锁后会注册一个定时任务监听锁，检查周期是：加锁失效时间的1/3，如加锁3s释放，检查是1s一次，加锁业务没执行完，会自动续期重置为加锁失效时间3s。requestId可以是当前线程id也可以唯一标识业务处理的id。

业务的机器万一宕机定时任务跑不了,就续不了期,那自然30秒之后锁就解开了。

```java
@Slf4j
@Service
public class RedisDistributionLockPlus {
 
    /**
     * 加锁超时时间，单位毫秒， 即：加锁时间内执行完操作，如果未完成会有并发现象
     */
    private static final long DEFAULT_LOCK_TIMEOUT = 30;
 
    private static final long TIME_SECONDS_FIVE = 5 ;
 
    /**
     * 每个key的过期时间 {@link LockContent}
     */
    private Map<String, LockContent> lockContentMap = new ConcurrentHashMap<>(512);
 
    /**
     * redis执行成功的返回
     */
    private static final Long EXEC_SUCCESS = 1L;
 
    /**
     * 获取锁lua脚本， k1：获锁key, k2：续约耗时key, arg1:requestId，arg2：超时时间
     */
    private static final String LOCK_SCRIPT = "if redis.call('exists', KEYS[2]) == 1 then ARGV[2] = math.floor(redis.call('get', KEYS[2]) + 10) end " +
            "if redis.call('exists', KEYS[1]) == 0 then " +
               "local t = redis.call('set', KEYS[1], ARGV[1], 'EX', ARGV[2]) " +
               "for k, v in pairs(t) do " +
                 "if v == 'OK' then return tonumber(ARGV[2]) end " +
               "end " +
            "return 0 end";
 
    /**
     * 释放锁lua脚本, k1：获锁key, k2：续约耗时key, arg1:requestId，arg2：业务耗时 arg3: 业务开始设置的timeout
     */
    private static final String UNLOCK_SCRIPT = "if redis.call('get', KEYS[1]) == ARGV[1] then " +
            "local ctime = tonumber(ARGV[2]) " +
            "local biz_timeout = tonumber(ARGV[3]) " +
            "if ctime > 0 then  " +
               "if redis.call('exists', KEYS[2]) == 1 then " +
                   "local avg_time = redis.call('get', KEYS[2]) " +
                   "avg_time = (tonumber(avg_time) * 8 + ctime * 2)/10 " +
                   "if avg_time >= biz_timeout - 5 then redis.call('set', KEYS[2], avg_time, 'EX', 24*60*60) " +
                   "else redis.call('del', KEYS[2]) end " +
               "elseif ctime > biz_timeout -5 then redis.call('set', KEYS[2], ARGV[2], 'EX', 24*60*60) end " +
            "end " +
            "return redis.call('del', KEYS[1]) " +
            "else return 0 end";
    /**
     * 续约lua脚本
     */
    private static final String RENEW_SCRIPT = "if redis.call('get', KEYS[1]) == ARGV[1] then return redis.call('expire', KEYS[1], ARGV[2]) else return 0 end";
 
 
    private final StringRedisTemplate redisTemplate;
 
    public RedisDistributionLockPlus(StringRedisTemplate redisTemplate) {
        this.redisTemplate = redisTemplate;
        ScheduleTask task = new ScheduleTask(this, lockContentMap);
        // 启动定时任务
        ScheduleExecutor.schedule(task, 1, 1, TimeUnit.SECONDS);
    }
 
    /**
     * 加锁
     * 取到锁加锁，取不到锁一直等待知道获得锁
     *
     * @param lockKey
     * @param requestId 全局唯一
     * @param expire   锁过期时间, 单位秒
     * @return
     */
    public boolean lock(String lockKey, String requestId, long expire) {
        log.info("开始执行加锁, lockKey ={}, requestId={}", lockKey, requestId);
        for (; ; ) {
            // 判断是否已经有线程持有锁，减少redis的压力
            LockContent lockContentOld = lockContentMap.get(lockKey);
            boolean unLocked = null == lockContentOld;
            // 如果没有被锁，就获取锁
            if (unLocked) {
                long startTime = System.currentTimeMillis();
                // 计算超时时间
                long bizExpire = expire == 0L ? DEFAULT_LOCK_TIMEOUT : expire;
                String lockKeyRenew = lockKey + "_renew";
 
                RedisScript<Long> script = RedisScript.of(LOCK_SCRIPT, Long.class);
                List<String> keys = new ArrayList<>();
                keys.add(lockKey);
                keys.add(lockKeyRenew);
                Long lockExpire = redisTemplate.execute(script, keys, requestId, Long.toString(bizExpire));
                if (null != lockExpire && lockExpire > 0) {
                    // 将锁放入map
                    LockContent lockContent = new LockContent();
                    lockContent.setStartTime(startTime);
                    lockContent.setLockExpire(lockExpire);
                    lockContent.setExpireTime(startTime + lockExpire * 1000);
                    lockContent.setRequestId(requestId);
                    lockContent.setThread(Thread.currentThread());
                    lockContent.setBizExpire(bizExpire);
                    lockContent.setLockCount(1);
                    lockContentMap.put(lockKey, lockContent);
                    log.info("加锁成功, lockKey ={}, requestId={}", lockKey, requestId);
                    return true;
                }
            }
            // 重复获取锁，在线程池中由于线程复用，线程相等并不能确定是该线程的锁
            if (Thread.currentThread() == lockContentOld.getThread()
                      && requestId.equals(lockContentOld.getRequestId())){
                // 计数 +1
                lockContentOld.setLockCount(lockContentOld.getLockCount()+1);
                return true;
            }
 
            // 如果被锁或获取锁失败，则等待100毫秒
            try {
                TimeUnit.MILLISECONDS.sleep(100);
            } catch (InterruptedException e) {
                // 这里用lombok 有问题
                log.error("获取redis 锁失败, lockKey ={}, requestId={}", lockKey, requestId, e);
                return false;
            }
        }
    }
 
 
    /**
     * 解锁
     *
     * @param lockKey
     * @param lockValue
     */
    public boolean unlock(String lockKey, String lockValue) {
        String lockKeyRenew = lockKey + "_renew";
        LockContent lockContent = lockContentMap.get(lockKey);
 
        long consumeTime;
        if (null == lockContent) {
            consumeTime = 0L;
        } else if (lockValue.equals(lockContent.getRequestId())) {
            int lockCount = lockContent.getLockCount();
            // 每次释放锁， 计数 -1，减到0时删除redis上的key
            if (--lockCount > 0) {
                lockContent.setLockCount(lockCount);
                return false;
            }
            consumeTime = (System.currentTimeMillis() - lockContent.getStartTime()) / 1000;
        } else {
            log.info("释放锁失败，不是自己的锁。");
            return false;
        }
 
        // 删除已完成key，先删除本地缓存，减少redis压力, 分布式锁，只有一个，所以这里不加锁
        lockContentMap.remove(lockKey);
 
        RedisScript<Long> script = RedisScript.of(UNLOCK_SCRIPT, Long.class);
        List<String> keys = new ArrayList<>();
        keys.add(lockKey);
        keys.add(lockKeyRenew);
 
        Long result = redisTemplate.execute(script, keys, lockValue, Long.toString(consumeTime),
                Long.toString(lockContent.getBizExpire()));
        return EXEC_SUCCESS.equals(result);
 
    }
 
    /**
     * 续约
     *
     * @param lockKey
     * @param lockContent
     * @return true:续约成功，false:续约失败（1、续约期间执行完成，锁被释放 2、不是自己的锁，3、续约期间锁过期了（未解决））
     */
    public boolean renew(String lockKey, LockContent lockContent) {
 
        // 检测执行业务线程的状态
        Thread.State state = lockContent.getThread().getState();
        if (Thread.State.TERMINATED == state) {
            log.info("执行业务的线程已终止,不再续约 lockKey ={}, lockContent={}", lockKey, lockContent);
            return false;
        }
 
        String requestId = lockContent.getRequestId();
        long timeOut = (lockContent.getExpireTime() - lockContent.getStartTime()) / 1000;
 
        RedisScript<Long> script = RedisScript.of(RENEW_SCRIPT, Long.class);
        List<String> keys = new ArrayList<>();
        keys.add(lockKey);
 
        Long result = redisTemplate.execute(script, keys, requestId, Long.toString(timeOut));
        log.info("续约结果，True成功，False失败 lockKey ={}, result={}", lockKey, EXEC_SUCCESS.equals(result));
        return EXEC_SUCCESS.equals(result);
    }
 
 
    static class ScheduleExecutor {
 
        public static void schedule(ScheduleTask task, long initialDelay, long period, TimeUnit unit) {
            long delay = unit.toMillis(initialDelay);
            long period_ = unit.toMillis(period);
            // 定时执行
            new Timer("Lock-Renew-Task").schedule(task, delay, period_);
        }
    }
 
    static class ScheduleTask extends TimerTask {
 
        private final RedisDistributionLockPlus redisDistributionLock;
        private final Map<String, LockContent> lockContentMap;
 
        public ScheduleTask(RedisDistributionLockPlus redisDistributionLock, Map<String, LockContent> lockContentMap) {
            this.redisDistributionLock = redisDistributionLock;
            this.lockContentMap = lockContentMap;
        }
 
        @Override
        public void run() {
            if (lockContentMap.isEmpty()) {
                return;
            }
            Set<Map.Entry<String, LockContent>> entries = lockContentMap.entrySet();
            for (Map.Entry<String, LockContent> entry : entries) {
                String lockKey = entry.getKey();
                LockContent lockContent = entry.getValue();
                long expireTime = lockContent.getExpireTime();
                // 减少线程池中任务数量
                if ((expireTime - System.currentTimeMillis())/ 1000 < TIME_SECONDS_FIVE) {
                    //线程池异步续约
                    ThreadPool.submit(() -> {
                        boolean renew = redisDistributionLock.renew(lockKey, lockContent);
                        if (renew) {
                            long expireTimeNew = lockContent.getStartTime() + (expireTime - lockContent.getStartTime()) * 2 - TIME_SECONDS_FIVE * 1000;
                            lockContent.setExpireTime(expireTimeNew);
                        } else {
                            // 续约失败，说明已经执行完 OR redis 出现问题
                            lockContentMap.remove(lockKey);
                        }
                    });
                }
            }
        }
    }
}
```



