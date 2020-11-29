Table of Contents
=================

* [Java基础](#java%E5%9F%BA%E7%A1%80)
  * [Keywords](#keywords)
    * [static](#static)
    * [new](#new)
    * [final](#final)
  * [数据类型](#%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)
    * [Boolean类型 null unbox问题](#boolean%E7%B1%BB%E5%9E%8B-null-unbox%E9%97%AE%E9%A2%98)
    * [Boolean\.TRUE 和 true  VS 性能](#booleantrue-%E5%92%8C-true--vs-%E6%80%A7%E8%83%BD)
    * [BigDecimal初始化和比较](#bigdecimal%E5%88%9D%E5%A7%8B%E5%8C%96%E5%92%8C%E6%AF%94%E8%BE%83)
  * [Java参数值传递和引用传递](#java%E5%8F%82%E6%95%B0%E5%80%BC%E4%BC%A0%E9%80%92%E5%92%8C%E5%BC%95%E7%94%A8%E4%BC%A0%E9%80%92)
  * [序列化](#%E5%BA%8F%E5%88%97%E5%8C%96)
  * [带标签break、continue](#%E5%B8%A6%E6%A0%87%E7%AD%BEbreakcontinue)
  * [时间戳](#%E6%97%B6%E9%97%B4%E6%88%B3)
  * [数据结构](#%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84)
    * [List](#list)
    * [for\-each并发修改](#for-each%E5%B9%B6%E5%8F%91%E4%BF%AE%E6%94%B9)
    * [ListIterator遍历List满足条件添加元素](#listiterator%E9%81%8D%E5%8E%86list%E6%BB%A1%E8%B6%B3%E6%9D%A1%E4%BB%B6%E6%B7%BB%E5%8A%A0%E5%85%83%E7%B4%A0)
    * [ListIterator源码](#listiterator%E6%BA%90%E7%A0%81)
    * [ListResourceBundle类实现国际化](#listresourcebundle%E7%B1%BB%E5%AE%9E%E7%8E%B0%E5%9B%BD%E9%99%85%E5%8C%96)
    * [List转Map](#list%E8%BD%ACmap)
    * [Java8 List转Map后，key相同，将不同value合并成List](#java8-list%E8%BD%ACmap%E5%90%8Ekey%E7%9B%B8%E5%90%8C%E5%B0%86%E4%B8%8D%E5%90%8Cvalue%E5%90%88%E5%B9%B6%E6%88%90list)
    * [ArrayList插入大量元素时，在插入前调用ensureCapacity增加ArrayList容量以提高插入效率](#arraylist%E6%8F%92%E5%85%A5%E5%A4%A7%E9%87%8F%E5%85%83%E7%B4%A0%E6%97%B6%E5%9C%A8%E6%8F%92%E5%85%A5%E5%89%8D%E8%B0%83%E7%94%A8ensurecapacity%E5%A2%9E%E5%8A%A0arraylist%E5%AE%B9%E9%87%8F%E4%BB%A5%E6%8F%90%E9%AB%98%E6%8F%92%E5%85%A5%E6%95%88%E7%8E%87)
    * [List Set Map Collection之间相互转化](#list-set-map-collection%E4%B9%8B%E9%97%B4%E7%9B%B8%E4%BA%92%E8%BD%AC%E5%8C%96)
    * [List满足条件的元素替换 Collections\.replaceAll](#list%E6%BB%A1%E8%B6%B3%E6%9D%A1%E4%BB%B6%E7%9A%84%E5%85%83%E7%B4%A0%E6%9B%BF%E6%8D%A2-collectionsreplaceall)
    * [List 和 List&lt;?&gt;](#list-%E5%92%8C-list)
    * [Collection\.synchronized( )使用注意](#collectionsynchronized-%E4%BD%BF%E7%94%A8%E6%B3%A8%E6%84%8F)
    * [JDK 1\.7 HasMap的头插死循环原因](#jdk-17-hasmap%E7%9A%84%E5%A4%B4%E6%8F%92%E6%AD%BB%E5%BE%AA%E7%8E%AF%E5%8E%9F%E5%9B%A0)
  * [注解](#%E6%B3%A8%E8%A7%A3)
    * [@SuppressWarnings(\{ "rawtypes", "unchecked" \})](#suppresswarnings-rawtypes-unchecked-)
    * [自定义注解](#%E8%87%AA%E5%AE%9A%E4%B9%89%E6%B3%A8%E8%A7%A3)
  * [SPI Service Provider Interface](#spi-service-provider-interface)
  * [POI](#poi)
    * [导出Word解决方案](#%E5%AF%BC%E5%87%BAword%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88)
  * [Java Agent](#java-agent)
    * [BTrace原理](#btrace%E5%8E%9F%E7%90%86)
    * [Arthas加Log调试](#arthas%E5%8A%A0log%E8%B0%83%E8%AF%95)
  * [JMS规范](#jms%E8%A7%84%E8%8C%83)
  * [JMS  VS MQ](#jms--vs-mq)

Created by [gh-md-toc](https://github.com/ekalinin/github-markdown-toc.go)

作者：cj

# Java基础

## Keywords

### static

静态代码块能包含this或者super？ 不能

当类加载器将类加载到JVM中的时候就会创建静态变量，这跟对象是否创建无关。静态变量加载的时候就会分配内存空间。静态代码块的代码只会在类第一次初始化的时候执行一次。一个类可以有多个静态代码块，它并不是类的成员，也没有返回值，并且不能直接调用。静态代码块不能包含this或者super,它们通常被用初始化静态变量。

### new



### final



## 数据类型

```java
public static void main(String[] args){
	Integer f1 = 100, f2 = 100, f3 = 150, f4 = 150;
	System.out.print(f1 == f2);
	System.out.print(f3 == f4);
}
== byte,short,char,int,long,float,double,boolean比的是stack中的值
== 引用类型比的是reference address
Object.equals()默认是 ==
```

IntegerCache 是 Integer 的内部类。整型字面量的值在-128 到 127 之间，不会 new 新的 Integer 对象，而是直接引用常量池中的 Integer 对象，所以 f1== f2 的结果是 true，而 f3 ==f4 的结果是 false

### Boolean类型 null unbox问题

```java
// 对null unbox会报错
public class Test {
    
    public static void main(String[] args) {
        Boolean a = true;
        Boolean b = true;
        Boolean c = null;
        if (Boolean.TRUE == new Boolean(true)) {
            System.out.println("==");
        }
        if (Boolean.TRUE.equals(b)) {
            System.out.println("equals");
        }
        Person p = new Person();
        System.out.println(a == b); // true
        System.out.println(a.equals(b));// true
        System.out.println(a == Boolean.TRUE);// true

        // java.lang.NullPointerException
        if (p.getIsTrustWorthy()) {
            System.out.println("");
        }
        System.out.println(p.getIsTrustWorthy() == true);
    }
}

@Data
class Person {
    private Boolean isTrustWorthy;

    public Person() {
    }

    public Person(Boolean isTrustWorthy) {
        this.isTrustWorthy = isTrustWorthy;
    }
}
```

### Boolean.TRUE 和 true  VS 性能

```java
// 避免box和unbox带来的性能损耗
public class Test {

    public static void main(String[] args) {
        NewClass n = new NewClass();

        long sysTime = System.currentTimeMillis();

        Runtime rt = Runtime.getRuntime();
        long freeMem = rt.freeMemory();
        System.out.println( "Free Memory before start --> " + freeMem );
        for( int i = 0; i < Integer.MAX_VALUE; i++ ){
            n.isItTrue();
        }
        System.out.println( "Time taken in Secs --> " + (System.currentTimeMillis() - sysTime)/1000D);
        System.out.println( "Free Memory After Process --> " + rt.freeMemory() );
        System.out.println( "Memory Usage --> " + ( freeMem - rt.freeMemory() ) );
    }
}

class NewClass {
    /**
     * Free Memory before start --> 250246800
     * Time taken in Secs --> 0.007
     * Free Memory After Process --> 248904600
     * Memory Usage --> 1342200
     */
    // boolean isItTrue(){
    //     return true;
    // }

    /**
     * Free Memory before start --> 250246800
     * Time taken in Secs --> 0.008
     * Free Memory After Process --> 248904600
     * Memory Usage --> 1342200
     */
    // Boolean isItTrue(){
    //     return true;
    // }

    /**
     *Free Memory before start --> 250246800
     * Time taken in Secs --> 0.007
     * Free Memory After Process --> 248904600
     * Memory Usage --> 1342200
     */
    // Boolean isItTrue(){
    //     return Boolean.TRUE;
    // }

    /**
     * Free Memory before start --> 250246800
     * Time taken in Secs --> 0.01
     * Free Memory After Process --> 248904600
     * Memory Usage --> 1342200
     */
    boolean isItTrue(){
        return Boolean.TRUE;
    }
}
```

### BigDecimal初始化和比较

```java
BigDecimal b1 = new BigDecimal(0.1);// 0.1不能用二进制精确表示，错误
BigDecimal b2 = new BigDecimal(0.5);// 0.5可以用二进制0.1精确表示，值没错

// 正确 推荐
BigDecimal b1 = new BigDecimal("0.1");
// 正确 推荐
BigDecimal b1 = BigDecimal.valueOf(0.1);

bigdecimal1.compareTo(bigdecimal2)
```



## Java参数值传递和引用传递

```css
参数值传递：传递到方法中的数据是参数副本，方法内对参数修改不会影响外部变量。
受影响：8种基本类型和String。

参数引用传递：传递到方法中的数据是参数引用，内部对参数修改也会作用到外部。
受影响：除String和8种基本类型的包装类以外其他所有对象类型、数组类型。
```

## 序列化

什么是序列化？Java对象转成字节流、转化成二进制序列、转化成字节序列？

为什么Java序列化慢？

Java本身并不支持跨语言，序列化版本号，类名等信息导致流变大肯定慢。 

为什么Protobuf快？

（1）T-V and T-L-V 每个字段用tag|leg|value或tag|value存储，tag记录value对应字段编号和value的数据类型，tag是二进制byte存储，一般只占一个byte，与key/value不同的是：key是字符串，每个字符就会占一个byte，Ex.name这个key就会占4个byte。string类型中leg记录字符串长度，避免了字符串定长的空间浪费（2）Varint以不同的长度来存储整数，ZigZag压缩将整数通过一个 hash 函数h(n) = (n<<1)^(n>>31)（如果是 sint64 h(n) = (n<<1)^(n>>63)），通过 ZigZag 编码，只要绝对值小的数字，都可以用较少位的 byte 表示。解决了负数的 Varint 位数会比较长的问题。而其他序列化一般是4个字节来表示整数，实际上较小的整数1个byte就够用了（3）陈硕根据 GPB 的 C++ 版本源代码分析出其反射的具体机制：DescriptorPool类根据 type name 拿到一个 Descriptor的对象指针，在通过MessageFactory工厂类根据Descriptor实例构造出具体的Message对象。

```protobuf
message Person {
  int32 id = 1;
  string name = 2;
}
id字段的field为1，writetype为int32类型对应的序号。编码后id对应的 Tag 为 (field_number << 3) | wire_type = 0000 1000，其中低位的 3 位标识 writetype，其他位标识field。
```

static 和 transient 的成员变量，不能被序列化。

父类被序列化，其子类也可以被序列化。

实现序列化接口的类中依赖枚举，枚举也必须实现序列化接口。

什么情况下需序列化？网络传输、缓存操作、持久到文件IO。

都用默认的序列化id有什么坑？两个类的功能代码完全一致，但是序列化 ID 不同，他们无法相互序列化和反序列化。

项目大时，不同子项目A和B依赖同一个类ClassXX，子项目A编译时ClassXX自动生成一个serialVersionUID作为序列化版本，项目B因改动需求，需要在本地类ClassXX添加字段，子项目A未重新编译导致反序列化失败java.io.InvalidClassException。

序列化id的运用：Client 端通过 Facade Object与业务逻辑对象进行交互，客户端的 Facade Object 不能直接由 Client 生成，需Server 端生成后网络传输给Client。Server 端进行版本更新时，将Server 端的 Facade Object的序列化 ID 再次生成，当 Client 端反序列化 Façade Object 会失败，目的是强制 Client 端从Server 端获取最新程序。

Q：多个实体类用同一个序列化id会发生什么？

## 带标签break、continue



## 时间戳

时间戳是距离1970年的毫秒数。

数据库timestamp和时区无关，比较范围可以用date类型比较，用dateStr不准(数据库时区和服务机器时区不同时有时间差问题)

## 数据结构

### List

### for-each并发修改

```java
// 错误一：删
public static void remove(ArrayList<String> list) 
{
    for (int i = 0; i < list.size(); i++) 
    {
        String s = list.get(i);
        if (s.equals("b")) 
        {
            list.remove(s);
        }
    }
}
// 错误二：删
public static void remove(ArrayList<String> list) 
{
    for (String s : list)
    {
        if (s.equals("b")) 
        {
            list.remove(s);
        }
    }
}
```

### ListIterator遍历List满足条件添加元素

```java
public class ListTest {
     public static void main(String[] args) {
        List list = new LinkedList();
        list.add("a");
        list.add("b");
        list.add("c");
        Iterator iter = list.iterator();
        while(iter.hasNext()) {
            String str = (String)iter.next();//ConcurrentModificationException并发修改异常
            if(str.equals("c")) {
                list.add("d");
            }
        }
        System.out.println(list.size());
    }
}
```

```java
Exception in thread "main" java.util.ConcurrentModificationException
	at java.util.LinkedList$ListItr.checkForComodification(LinkedList.java:966)
	at java.util.LinkedList$ListItr.next(LinkedList.java:888)
	at org.union.eastday.aop.ListTest.main(ListTest.java:15)
```

应采用 ListIterator

```java
public static void main(String[] args) {
        List list = new ArrayList();
        list.add("a");
        list.add("b");
        list.add("c");

        ListIterator listIterator = list.listIterator();
        while (listIterator.hasNext()) {
            String str = (String) listIterator.next();
            if (str.equals("c")) {
                listIterator.add("d");
            }
        }
        System.out.println(list);
    }
```

### ListIterator源码

```java
public interface ListIterator<E> extends Iterator<E> {
    // Query Operations

    /**
     * Returns {@code true} if this list iterator has more elements when
     * traversing the list in the forward direction. (In other words,
     * returns {@code true} if {@link #next} would return an element rather
     * than throwing an exception.)
     *
     * @return {@code true} if the list iterator has more elements when
     *         traversing the list in the forward direction
     */
    boolean hasNext();

    /**
     * Returns the next element in the list and advances the cursor position.
     * This method may be called repeatedly to iterate through the list,
     * or intermixed with calls to {@link #previous} to go back and forth.
     * (Note that alternating calls to {@code next} and {@code previous}
     * will return the same element repeatedly.)
     *
     * @return the next element in the list
     * @throws NoSuchElementException if the iteration has no next element
     */
    E next();

    /**
     * Returns {@code true} if this list iterator has more elements when
     * traversing the list in the reverse direction.  (In other words,
     * returns {@code true} if {@link #previous} would return an element
     * rather than throwing an exception.)
     *
     * @return {@code true} if the list iterator has more elements when
     *         traversing the list in the reverse direction
     */
    boolean hasPrevious();

    /**
     * Returns the previous element in the list and moves the cursor
     * position backwards.  This method may be called repeatedly to
     * iterate through the list backwards, or intermixed with calls to
     * {@link #next} to go back and forth.  (Note that alternating calls
     * to {@code next} and {@code previous} will return the same
     * element repeatedly.)
     *
     * @return the previous element in the list
     * @throws NoSuchElementException if the iteration has no previous
     *         element
     */
    E previous();

    /**
     * Returns the index of the element that would be returned by a
     * subsequent call to {@link #next}. (Returns list size if the list
     * iterator is at the end of the list.)
     *
     * @return the index of the element that would be returned by a
     *         subsequent call to {@code next}, or list size if the list
     *         iterator is at the end of the list
     */
    int nextIndex();

    /**
     * Returns the index of the element that would be returned by a
     * subsequent call to {@link #previous}. (Returns -1 if the list
     * iterator is at the beginning of the list.)
     *
     * @return the index of the element that would be returned by a
     *         subsequent call to {@code previous}, or -1 if the list
     *         iterator is at the beginning of the list
     */
    int previousIndex();


    // Modification Operations

    /**
     * Removes from the list the last element that was returned by {@link
     * #next} or {@link #previous} (optional operation).  This call can
     * only be made once per call to {@code next} or {@code previous}.
     * It can be made only if {@link #add} has not been
     * called after the last call to {@code next} or {@code previous}.
     *
     * @throws UnsupportedOperationException if the {@code remove}
     *         operation is not supported by this list iterator
     * @throws IllegalStateException if neither {@code next} nor
     *         {@code previous} have been called, or {@code remove} or
     *         {@code add} have been called after the last call to
     *         {@code next} or {@code previous}
     */
    void remove();

    /**
     * Replaces the last element returned by {@link #next} or
     * {@link #previous} with the specified element (optional operation).
     * This call can be made only if neither {@link #remove} nor {@link
     * #add} have been called after the last call to {@code next} or
     * {@code previous}.
     *
     * @param e the element with which to replace the last element returned by
     *          {@code next} or {@code previous}
     * @throws UnsupportedOperationException if the {@code set} operation
     *         is not supported by this list iterator
     * @throws ClassCastException if the class of the specified element
     *         prevents it from being added to this list
     * @throws IllegalArgumentException if some aspect of the specified
     *         element prevents it from being added to this list
     * @throws IllegalStateException if neither {@code next} nor
     *         {@code previous} have been called, or {@code remove} or
     *         {@code add} have been called after the last call to
     *         {@code next} or {@code previous}
     */
    void set(E e);

    /**
     * Inserts the specified element into the list (optional operation).
     * The element is inserted immediately before the element that
     * would be returned by {@link #next}, if any, and after the element
     * that would be returned by {@link #previous}, if any.  (If the
     * list contains no elements, the new element becomes the sole element
     * on the list.)  The new element is inserted before the implicit
     * cursor: a subsequent call to {@code next} would be unaffected, and a
     * subsequent call to {@code previous} would return the new element.
     * (This call increases by one the value that would be returned by a
     * call to {@code nextIndex} or {@code previousIndex}.)
     *
     * @param e the element to insert
     * @throws UnsupportedOperationException if the {@code add} method is
     *         not supported by this list iterator
     * @throws ClassCastException if the class of the specified element
     *         prevents it from being added to this list
     * @throws IllegalArgumentException if some aspect of this element
     *         prevents it from being added to this list
     */
    void add(E e);
}
```

### ListResourceBundle类实现国际化

### List转Map

```java
Map<Long, String> maps = userList.stream().collect(Collectors.toMap(User::getId, User::getAge, (key1, key2) -> key2));

Guava Map<Long, User> maps = Maps.uniqueIndex(userList, new Function<User, Long>() {
            @Override
            public Long apply(User user) {
                return user.getId();
            }
   });

Map<Long, User> maps = userList.stream().collect(Collectors.toMap(User::getId,Function.identity()));当getId key一样时报错，应采用 Map<Long, User> maps = userList.stream().collect(Collectors.toMap(User::getId, Function.identity(), (key1, key2) -> key2));

```

### Java8 List转Map后，key相同，将不同value合并成List

```java
List<SysMenu> menuList = new ArrayList<>();
Map<String, List<SysMenu>> menuMap = menutList.stream().collect(Collectors.toMap(SysMenu::getParentId, menuObj ->
Lists.newArrayList(menuObj), (List<SysMenu> newValueList, List<SysMenu> oldValueList) ->
{
    oldValueList.addAll(newValueList);
    return oldValueList;
}));
```

### ArrayList插入大量元素时，在插入前调用ensureCapacity增加ArrayList容量以提高插入效率



### List Set Map Collection之间相互转化

http://www.360doc.com/content/16/0113/15/26839592_527616462.shtml

### List满足条件的元素替换 Collections.replaceAll

```java
public static void main(String[] args) {
	  List list = Arrays.asList("one Two three Four five six one three Four".split(" "));
      System.out.println("List :"+list);
      Collections.replaceAll(list, "one", "hundrea");
      System.out.println("replaceAll: " + list);
   }
}
```

### List<T> 和 List<?>

```
List<T> 泛型一种情况，List<?>不确定泛型类型
```

### Collection.synchronized( )使用注意

```java
List list = Collections.synchronizedList(new ArrayList());
      ...
  synchronized(list) {
      Iterator i = list.iterator(); // Must be in synchronized block，再进行一次同步，防止其他线程修改集合元素
      while (i.hasNext())
          foo(i.next());
  }
// 若list可序列化，则返回列表也是可序列化
```

### JDK 1.7 HasMap的头插死循环原因

```java
void resize(int newCapacity)
{
    Entry[] oldTable = table;
    int oldCapacity = oldTable.length;
    ......
    //创建一个新的Hash Table
    Entry[] newTable = new Entry[newCapacity];
    //将Old Hash Table上的数据迁移到New Hash Table上
    transfer(newTable);
    table = newTable;
    threshold = (int)(newCapacity * loadFactor);
}

void transfer(Entry[] newTable)
{
　　//复制一个原数组src，Entry是一个静态内部类，有K，V，next三个成员变量
    Entry[] src = table;
　　//数组新容量
    int newCapacity = newTable.length;
    //  从OldTable里摘一个元素出来，然后放到NewTable中
    for (int j = 0; j < src.length; j++) {
        Entry<K,V> e = src[j];//取出原数组一个元素
        if (e != null) {//判断原数组该位置有元素
            src[j] = null;//原数组位置置为空
            do {//对原数组某一位置下的一串元素进行操作
                Entry<K,V> next = e.next;//next是当前元素下一个
                int i = indexFor(e.hash, newCapacity);//i是元素在新数组的位置
                e.next = newTable[i];//此处体现了头插法，当前元素的下一个是新数组的头元素
                newTable[i] = e;//将原数组元素加入新数组
                e = next;//遍历到原数组某一位置下的一串元素的下一个
　　　　　　} while (e != null); 
　　　　} 
　　} 
}
```



## 注解

### @SuppressWarnings({ "rawtypes", "unchecked" })

```java
@SuppressWarnings({ "rawtypes", "unchecked" })告诉编译器忽略指定的警告，不用在编译完成后出现警告信息
```

```java
        List strList = new ArrayList();
        strList.add("a");
        String str = (String) strList.get(0);
        System.out.println(str);

        List<String> strList2 = new ArrayList<>();
        strList2.add("a");
        String str2 = strList2.get(0);
        System.out.println(str2);
```

### 自定义注解

```

```

## SPI Service Provider Interface

使用场景：服务接口与服务实现分离解耦，提升程序可扩展性。上游系统调下游系统，让上游在Jar包中打一个SPI接口，下游业务实现这个SPI接口，上游调用这一个接口可以使用下游不同的功能。

每一个SPI接口都需要在自己项目的静态资源目录中声明一个services文件，文件名为规范接口的类名全路径，格式{companyDomainSuffix}.{projectName}.{interfaceName}，文件内容是具体实现的全路径{companyDomainSuffix}.{projectName}.{concretInterfaceImplementation}

```java
Ex.
resources\META-INF\services\路径下创建一个名为com.kritter.spi.api.Printer文件
resources\META-INF\services\com.kritter.spi.api.Printer

Printer文件类容为
com.kritter.spi.api.ColorPrinter
    
Dubbo也支持JavaSPI，对JavaSPI做了优化，不会直接将全部类加载到内存。Dubbo spi支持adaptive active等。
```

## POI

### 导出Word解决方案

```css
(1)Jacob Java-COM Bridge 自带DLL动态链接库，并通过JNI实现了在Java平台上对COM程序的调用，局限DLL依赖于Windows。
(2)Apache POI 基于MicroSoft OLE 2 Compound Document Format的各种格式文件，在Java中读写Excel、Word。处理Excel强大。处理Word局限于读取，只能实现简单文件操作，不能设置样式。市面使用较多，不错的选型。
(3)Java2word 在Java中调用 MS Office Word组件类库，可动态排版word文档，指定文本样式，指定表格样式。
(4)iText是开源sourceforge，生成PDF，可以将XML、Html转化为PDF。
(5)JSP输出样式，处理样式有缺陷，过老的技术。
(6)Office2003(2003才开始支持XML)或者2007编辑好Word样式，另存为XML，将XML翻译成FreeMarker，Java解析FreeMarker并输出Doc，流程有点长。
```



## Java Agent

```
线上问题经常需加log调试，改代码打包部署太费力，在服务器上直接改代码使之实时生效
java.lang.instrument.Instrumentation提供了在运行时重新加载某个类class文件的API

两种方式拿到Instrumentation
(1)在JVM启动时指定agent，Instrumentation会通过agent#premain方法传递，缺陷是改一次agent，需要重启一下这个服务的JVM
(2)
```

### BTrace原理

```
动态字节码修改技术Instrumentation来实现运行时Java程序跟踪和替换。
Client(Java compile api + attach api) + Agent(脚本解析引擎 + ASM + JDK6 Instumentation) + Socket
```



### Arthas加Log调试

```shell
#下载arthas agent
wget https://alibaba.github.io/arthas/arthas-boot.jar

#启动agent
java -jar arthas-boot.jar --target-ip 0.0.0.0

#sc：search class 查找类文件
sc *SelectionController

#jad 反编译class 并输出到文件
jad --source-only com.acfun.controller.SelectionController > /tmp/SelectionController.java

#修改源代码
vi /tmp/SelectionController.java

#sc查找加载UserController的ClassLoader  -d参数可以打印出类加载的具体信息
sc -d *SelectionController |grep classLoaderHash 

#编译源代码 使用mc(Memory Compiler)命令来编译，并且通过-c参数指定ClassLoader
mc -c 3787f831 /tmp/SelectionController.java -d /tmp

#使用redefine命令重新加载新编译好的class
redefine /tmp/com/acfun/controller/SelectionController.class

#redefine成功之后，访问controller，观察代码是否生效
```

## JMS规范

```css
适用场景：
(1)A和B两个应用服务之间对各自都不了解，部署跨不同的机架。当A触发某事件后，B想从A获取一些更新信息。可能不止一个B对A更新感兴趣，N个B感兴趣。
(2)
```

## JMS  VS MQ

```
JMS Java Messaging Service是面向消息中间件(MOM)的技术规范
MQ是面向消息中间件(MOM)的最终实现
```

