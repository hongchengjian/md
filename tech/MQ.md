

Table of Contents
=================

* [MQ](#mq)
  * [为什么要用MQ？](#%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E7%94%A8mq)
  * [消息协议](#%E6%B6%88%E6%81%AF%E5%8D%8F%E8%AE%AE)
    * [TCP](#tcp)
    * [MQTT](#mqtt)
    * [AMQP](#amqp)
    * [RTMP](#rtmp)
  * [消息模式](#%E6%B6%88%E6%81%AF%E6%A8%A1%E5%BC%8F)
  * [VS](#vs)
  * [常见发送问题和错误方案：](#%E5%B8%B8%E8%A7%81%E5%8F%91%E9%80%81%E9%97%AE%E9%A2%98%E5%92%8C%E9%94%99%E8%AF%AF%E6%96%B9%E6%A1%88)
  * [常见消费失败问题：](#%E5%B8%B8%E8%A7%81%E6%B6%88%E8%B4%B9%E5%A4%B1%E8%B4%A5%E9%97%AE%E9%A2%98)
    * [（1）Kafka](#1kafka)
    * [（2）RabbitMQ](#2rabbitmq)
  * [Kafka](#kafka)
    * [定义和适用场景](#%E5%AE%9A%E4%B9%89%E5%92%8C%E9%80%82%E7%94%A8%E5%9C%BA%E6%99%AF)
    * [架构](#%E6%9E%B6%E6%9E%84)
    * [命令行](#%E5%91%BD%E4%BB%A4%E8%A1%8C)
    * [server\.properties](#serverproperties)
    * [版本差异](#%E7%89%88%E6%9C%AC%E5%B7%AE%E5%BC%82)
    * [Kafka支持事务？](#kafka%E6%94%AF%E6%8C%81%E4%BA%8B%E5%8A%A1)
    * [Kafka支持消息优先级](#kafka%E6%94%AF%E6%8C%81%E6%B6%88%E6%81%AF%E4%BC%98%E5%85%88%E7%BA%A7)
    * [为什么Kafka那么快？](#%E4%B8%BA%E4%BB%80%E4%B9%88kafka%E9%82%A3%E4%B9%88%E5%BF%AB)
    * [Zero\-Copy 零拷贝](#zero-copy-%E9%9B%B6%E6%8B%B7%E8%B4%9D)
      * [什么是Zero\-Copy 零拷贝？](#%E4%BB%80%E4%B9%88%E6%98%AFzero-copy-%E9%9B%B6%E6%8B%B7%E8%B4%9D)
      * [Zero\-Copy需要CPU？](#zero-copy%E9%9C%80%E8%A6%81cpu)
      * [Pull VS Post](#pull-vs-post)
    * [有序消费](#%E6%9C%89%E5%BA%8F%E6%B6%88%E8%B4%B9)
    * [ISR、AR代表什么？ISR伸缩？](#israr%E4%BB%A3%E8%A1%A8%E4%BB%80%E4%B9%88isr%E4%BC%B8%E7%BC%A9)
    * [Broker消息代理](#broker%E6%B6%88%E6%81%AF%E4%BB%A3%E7%90%86)
    * [Kafka选举基于Broker还是Group？](#kafka%E9%80%89%E4%B8%BE%E5%9F%BA%E4%BA%8Ebroker%E8%BF%98%E6%98%AFgroup)
    * [ConsumerGroup中新加Consumer、移除Consumer、Consumer崩溃时发生Rebalance](#consumergroup%E4%B8%AD%E6%96%B0%E5%8A%A0consumer%E7%A7%BB%E9%99%A4consumerconsumer%E5%B4%A9%E6%BA%83%E6%97%B6%E5%8F%91%E7%94%9Frebalance)
    * [Kafka为什么不将offset保存Broker维护？而是在Partition维护？](#kafka%E4%B8%BA%E4%BB%80%E4%B9%88%E4%B8%8D%E5%B0%86offset%E4%BF%9D%E5%AD%98broker%E7%BB%B4%E6%8A%A4%E8%80%8C%E6%98%AF%E5%9C%A8partition%E7%BB%B4%E6%8A%A4)
  * [RabbitMQ](#rabbitmq)
    * [模型](#%E6%A8%A1%E5%9E%8B)
    * [顺序消费(RabbitMQ本身缺少顺序消费机制)](#%E9%A1%BA%E5%BA%8F%E6%B6%88%E8%B4%B9rabbitmq%E6%9C%AC%E8%BA%AB%E7%BC%BA%E5%B0%91%E9%A1%BA%E5%BA%8F%E6%B6%88%E8%B4%B9%E6%9C%BA%E5%88%B6)
    * [重复消费出现场景](#%E9%87%8D%E5%A4%8D%E6%B6%88%E8%B4%B9%E5%87%BA%E7%8E%B0%E5%9C%BA%E6%99%AF)
    * [解决重复消费](#%E8%A7%A3%E5%86%B3%E9%87%8D%E5%A4%8D%E6%B6%88%E8%B4%B9)
    * [消费失败处理](#%E6%B6%88%E8%B4%B9%E5%A4%B1%E8%B4%A5%E5%A4%84%E7%90%86)
    * [死信队列原理](#%E6%AD%BB%E4%BF%A1%E9%98%9F%E5%88%97%E5%8E%9F%E7%90%86)
      * [死信几种情况](#%E6%AD%BB%E4%BF%A1%E5%87%A0%E7%A7%8D%E6%83%85%E5%86%B5)
    * [RabbitMQ的事务（Confirm模式要比事务快10倍）](#rabbitmq%E7%9A%84%E4%BA%8B%E5%8A%A1confirm%E6%A8%A1%E5%BC%8F%E8%A6%81%E6%AF%94%E4%BA%8B%E5%8A%A1%E5%BF%AB10%E5%80%8D)
      * [（1）AMQP的事务机制](#1amqp%E7%9A%84%E4%BA%8B%E5%8A%A1%E6%9C%BA%E5%88%B6)
      * [（2）发送者确认模式实现](#2%E5%8F%91%E9%80%81%E8%80%85%E7%A1%AE%E8%AE%A4%E6%A8%A1%E5%BC%8F%E5%AE%9E%E7%8E%B0)
  * [RocketMQ](#rocketmq)
    * [消息协议](#%E6%B6%88%E6%81%AF%E5%8D%8F%E8%AE%AE-1)
    * [事务原理](#%E4%BA%8B%E5%8A%A1%E5%8E%9F%E7%90%86)
    * [顺序消息原理](#%E9%A1%BA%E5%BA%8F%E6%B6%88%E6%81%AF%E5%8E%9F%E7%90%86)
    * [延时消息解决方案](#%E5%BB%B6%E6%97%B6%E6%B6%88%E6%81%AF%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88)
    * [延时消息场景](#%E5%BB%B6%E6%97%B6%E6%B6%88%E6%81%AF%E5%9C%BA%E6%99%AF)
    * [延时只支持18个level原理](#%E5%BB%B6%E6%97%B6%E5%8F%AA%E6%94%AF%E6%8C%8118%E4%B8%AAlevel%E5%8E%9F%E7%90%86)
    * [消费方式](#%E6%B6%88%E8%B4%B9%E6%96%B9%E5%BC%8F)
      * [集群消费（默认）](#%E9%9B%86%E7%BE%A4%E6%B6%88%E8%B4%B9%E9%BB%98%E8%AE%A4)
      * [广播消费](#%E5%B9%BF%E6%92%AD%E6%B6%88%E8%B4%B9)

Created by [gh-md-toc](https://github.com/ekalinin/github-markdown-toc.go)

作者：cj

# MQ

## 为什么要用MQ？

同步处理弊端：client、server必须同时在线才能通信，其中任意一个不在线就不能通信。

异步：存队列时不需要立即处理，在需要时取队列数据才处理，好处：（1）解耦，不需要两方同时在线（2）发的快，收的慢，削峰有助于控制和优化数据流经过系统的速度，解决生产消息和消费消息处理速度不一致，生产大于消费。

削峰：上游流量大、下游扛不住

冗余：一对多，一个生成者，多个订阅Topic

灵活性：动态上线、下线机器，比如加入双11

健壮：消息积压，系统一部分组件失效，不会影响到整个系统。即使一个处理消息的进程挂掉，加入队列中的消息仍然可以在系统恢复后被处理。

消息一致性：利用事务，账号转账如系统A扣钱，系统B加钱。

VS：数据库一致性是事务完成，所有数据具有一致状态。

CAP 分区容忍性partition tolerance：数据在不同网络子网，一个子网挂了，其他子网能访问到这个数据，常用保障方法是多个副本复制。

## 消息协议

### TCP

 Kafka

### MQTT

Message Queuing Telemetry Transport 消息队列遥测传输。基于TCP/IP。

### AMQP

RabbitMQ

### RTMP

## 消息模式

```css
(1)一对一：点对点 消费者主动拉取消息，消息收到后消息清除
类似Flume：消息可以给多个人，前提是Flume要多个channel、多个sink sink是绑定channel一个，事务完成了channel把数据清掉
消息生产者生产消息发送到Queue中，然后消费者从Queue中取出并且消费消息。消息被消费后，queue中不在有存储，所以消费者不可能消费到已经被消费的消息。
(2)Pub/Sub模式：一对多，消费者消费数据之后不会清除消息
消息生产者(Pub)将消息发布到topoc中，同时有多个消息消费者(Sub)消费该消息。和点对点不同，发布到topic的消息会被所有订阅者消费。
Ex.公众号管理员推数据给订阅者，推的问题：消息队列不能根据不同的消费者决定推送速度。生产者推给消息队列(瓶颈在生产者) ---> 消息队列推给消费者(瓶颈推由当前队列决定，Ex.消息队列固定推50M/s，而有的订阅者10M/s消费能力会被压崩，有的订阅者100M/s会造成资源浪费)

所以发布订阅模式中有另外一种消费模式：消费者主动拉取，Kafka是消费者主动拉取的模式，由消费者决定消费速度。拉取模式的缺点：（1）消费者需要长时间轮询队列是否有消息，比较浪费资源。即使没有消息时，需要长时间轮询队列是否有消息。（2）也可以不维护长轮询，消息队列多维护一个消费者的列表，当有新消息来时通知到消费者，前提是消息队列要知道有哪些消费者订阅了列表，这种情况下存在的问题是消息队列通知不到已挂的消费者
类似Flume：sink从channel长轮询看channel中是否有消息
```



## VS

```css
几种MQ优缺
点对点 VS Pub/Sub(pull VS push)
```



## 常见发送问题和错误方案：

(1)将发送消息网络调用和update DB放在同一个事务里，若发送消息失败，update DB自动回滚

A.发送消息失败，发送方并不知道消息中间件是否真的没收到消息（MQ消息已经收到，只是返回response时候失败了）

B.将网络调用放在事务DB中，因网络延时，导致DB长事务，严重会Block整个DB。

## 常见消费失败问题：

### （1）Kafka

Kafka消费时存在业务异常，暂不提交offset，保存消费失败的消息记录，根据失败策略处理相应消息。保存消费失败的消息记录后可以提交offset。

Kafka消费时网络异常，重试，超过重试次数进行人工处理。

失败策略处理：（1）定时重试（2）失败处理隔五分钟再往对应的消息队列发送该消息，发送成功后就次数+1，根据消息id定位消息，记录消息消费次数，达到次数的阀值改为人工处理。

### （2）RabbitMQ

消费失败的消息放入死信队列，仓储系统会开启一个独立的线程（当第三方系统服务正常的情况下）用来处理死信队列，该线程还需用来监控第三方系统服务的状态。

## Kafka

### 定义和适用场景

```css
kafka是一个分布式基于Pub/Sub模式的消息队列(先进先出顺序保证)，主要应用于大数据(收集日志、监控信息、埋点)实时处理领域。90%Spark Streaming数据来源于kafka。解耦、削峰，动态上下线(高峰临时突发情况，增加机器、换机器)， 暂存消息(A和B两个系统之间通信时缓冲速度不对等)
```

LinkIn研发处理流式数据，Kafka一个topic可以分成多个Partition，一个topic可以被多个group消费，**每个Partition只被一个消费组里的一个消费者消费**，Partition每个消息对应唯一的offset。

### 架构

```css
Flume:source, channel, sink
消息：一行数据
生产者
消费者

broker:服务器，只是服务器起了一个kafka进程；其中只做broker，不做消息分类，多个系统的消息数据会混合在一块
Topic:在broker里对数据做分类.(1)Topic有分区 Partition(2)每个分区Partition是有副本(Leader和Follower)

生产者往一个不存在的Topic里发消息也能发，系统会自己创建server.properties中定义的一个分区一个副本

Topic是逻辑概念，Partition是物理概念
log.segment.bytes=1073741824 对应 0000 0000 0000 0000 0000.log 只存消息数据 1G
二分查找法定位.index文件  0000 0000 0000 0000 0000.index
(1)超过1G时，产生新的文件如何命名？
(2)如何快速定位想要的数据？
由于Producer生产的Msg会不断追加到log文件末尾，为了防止log文件过大导致数据定位效率低下，Kafka采用分片和索引，将每个partition分为多个segment，每个segment对应两个文件 .index 和 .log

Partition:Ex.Partition 0和Partition 1，提供同一个Topic的负载均衡，提高并发度，同一个Topic的多个partition不是传给同一个机器
VS MR Partition(提高reducer并发度) VS Hive Partition(查询减少读取数据量)

副本数=Leader数+Follower数，副本包括了Leader和Follower。Leader针对的是Partition，不是针对集群的Leader，若Leader挂了，将另一个Follower提升为Leader，所以Leader和Follower一定不在同一台机器(同一个broker)，因为一台机器挂了，即使存多份在同一台也是没有意义的。Kafka有暂存功能，HDFS DataNode副本没有Leader和Follower，3台机器可以搞10个副本，DataNode中连任意一份副本都可以。而Kafka中生产者和消费者只找Leader不找Follower，Follower仅起备份。

Replication做副本数据冗余
副本作用是简单备份，副本的一致性概念

Consumer Group:多个消费可以放一个组，好处是提高消费消息能力
消费者组里的分区Partition分配策略
注意⚠️:一个Partition只能被一个消费者组Consumer Group里的某一个Consumer消费 
Ex1.在Topic A可以被Consumer A消费情况下，Topic A不能同时被Consumer B消费，但是Topic A可以同时被Consumer C消费(因Consumer A和Consumer C不在同一个Consumer Group)

Ex2.Consumer Group里若只有Consumer A(没有Consumer B)，Consumer A订阅的是Topic A的情况下，Topic A Patition 0和Topic A Patition 1都要被Consumer A消费，注意只连Leader，不会连Follower

Ex3.Consumer A、Consumer B、Consumer C都是订阅Topic A，Topic A有2个Partition情况下，则Consumer C空转浪费资源

消费者个数 > 主题的分区个数，浪费多出的消费者资源
并发度最好情况：消费者组里的个数和主题的分区数相等时
```



```css
记录offset作用：当消费出问题了，可以下次从中断处接着消费。
0.9版本之前offset存储在ZK
0.9版本之后offset存储在kafka本地(存储在系统创建的Topic，存在磁盘默认保留7天，不是存在内存)

为什么从ZK改到Kafka？
消费者要和Kafka集群中Topic Partition Leader通信，消费者拉取速度快必须和ZK交互频繁，并发高时ZK效率不高
```

### 命令行

```css
命令行一般做测试用，改文件../config/consumer.properties、server.properties，但在代码里一般直接写配置，不会改配置文件

命令行连的都是Zookeeper，消费者命令行有两种连法(1)偏移量0.9.x保存在Zookeeper(2)
生产者连的不是Zookeeper，
两种查 Topic和List，Create和Delete，增加的时候需要关注Topic的分区和副本数
```

### server.properties

```shell
# 必须是integer
Broker.id=0
# 可以删除topic
delete.topoc.enable=true
# kafka暂存数据的目录
log.dirs=/tmp/
# 数据保存时间
log.retention.hours=168

zookeeper.connection=hadoop101:11,hadoop102:12,hadoop103:13
```



### 版本差异

```css
Kafka 2.10/2.11 不是Kafka版本，而是Scala版本
Kafka Server端是Scala编写，Scala主流3个版本分别是2.10、2.11、2.12，Kafka现在每个PULL request都已经自动增加了这三个版本的检查
Kafka广泛使用的版本：0.8.x、0.9.x、0.10.* 
Kafka 0.9.x之前：提供ConsumerConnector、ZookeeperConsumerConnector以及SimpleConsumer，Consumer是Scala编写，包名结构是kafka.consumer.*，分为high-level consumer和low-level consumer 
Kafka 0.9.x开始提供Java版本的Consumer，新版本Consumer可以独立部署，不再需要依赖Server端代码，提供KafkaConsumer和ConsumerRecord，包名结构是o.a.k.clients.consumer.*
```

### Kafka支持事务？



### Kafka支持消息优先级



### 为什么Kafka那么快？

Pull、Zero-Copy、Partition

Pull模式与消费端处理能力相符

Zero-Copy 零拷贝技术

顺序写 Partition，一个Partition里的消息是有序的

### Zero-Copy 零拷贝

#### 什么是Zero-Copy 零拷贝？

#### Zero-Copy需要CPU？

不需要（从用户态到核心态切换的过程是CPU控制）

#### Pull VS Post



### 有序消费



### ISR、AR代表什么？ISR伸缩？

ISR：In-Sync Replicas副本同步队列，ISR由leader维护，follower从leader同步数据

AR：Assigned Replicas 所有副本

AR=ISR + OSR

### Broker消息代理

Producer往Broker里指定Topic中写消息，Consumers从Brokers里拉取指定Topic消息进行业务处理，Broker起到一个代理保存消息的中转站。

producer生产一条消息，存储到哪个broker server中

### Kafka选举基于Broker还是Group？

基于Broker

### ConsumerGroup中新加Consumer、移除Consumer、Consumer崩溃时发生Rebalance

Rebalance协议规定一个Consumer Group下所有Consumer 如何达成一致来分配订阅Topic下的每个Partition。

一个Group下20个Consumer，Group订阅了具100个Partition的Topic，正常情况经过Rebalance，平均每个

Consumer分配5个Partition。

### Kafka为什么不将offset保存Broker维护？而是在Partition维护？



## RabbitMQ

### 模型



### 顺序消费(RabbitMQ本身缺少顺序消费机制)

单个queue在多消费者下不能保证有序消费

### 重复消费出现场景

任务超时，没有及时返回状态，引起任务重新入队列后重新消费

连接断开也会触发重复消费

### 解决重复消费



### 消费失败处理

（1）消费失败的消息放入死信队列，开启独立线程（当第三方系统服务正常的情况下）用来处理死信队列，该线程还需用来监控第三方系统服务的状态。

（2）网络异常重试超过阀值进行熔断，业务异常切到具体业务异常code对应的处理机制中。兜底写库后尝试起定时任务和做开关重试。

### 死信队列原理

```
DLX dead-letter-exchange
```

#### 死信几种情况

```css
（1）消息被拒绝(basic.reject / basic.nack)，并且requeue = false
（2）消息TimeToLive TTL过期
$ curl -i -u guest:guest -H "content-type:application/json"  -XPUT -d'{"auto_delete":false,"durable":true,"arguments":{"x-message-ttl": 60000}}' 
（3）队列达到最大长度（rabbitMQ的积压能力比较落）
（4）消费失败时放入（可选情况）
```

### RabbitMQ的事务（Confirm模式要比事务快10倍）

#### （1）AMQP的事务机制

```java
Channel channel = conn.createChannel();
// 声明队列
channel.queueDeclare(_queueName, true, false, false, null);
String message = String.format("时间 => %s", new Date().getTime());
try {
	channel.txSelect(); // 声明事务
	// 发送消息
	channel.basicPublish("", _queueName, MessageProperties.PERSISTENT_TEXT_PLAIN, message.getBytes("UTF-8"));
	channel.txCommit(); // 提交事务
} catch (Exception e) {
	channel.txRollback();
} finally {
	channel.close();
	conn.close();
}
抓包步骤：
（1）Client端向Server端发 Tx.Select
（2）Server端返回Tx.Select-OK
（3）Client端推送消息
（4）客户端发送给事务提交Tx.Commit
（5）服务端返回Tx.Commit-OK

消费端若使用了事务，autoAck=false，手动确认后回滚Rollback了事务，此条消息会重新放回队列。autoAck=true，手动确认后回滚Rollback了事务，队列已经把消息移除了。
```

#### （2）发送者确认模式实现

Confirm机制3种：

```css
channel.waitForConfirms()普通发送方确认模式
Confirm批量确定和Confirm异步模式性能相差不大
channel.waitForConfirmsOrDie()批量确认模式，只要批次中有一个消息未被确认就会抛出IOException
channel.addConfirmListener()异步监听发送方确认模式，执行效率高
```



## RocketMQ

### 消息协议



### 事务原理



### 顺序消息原理

消息有序指的是一类消息消费时，能按照发送的顺序来消费。

### 延时消息解决方案

定时器Timer，延时队列DelayQueue

### 延时消息场景

提交了一个订单就发送一个延时消息，1h后去检查这个订单的状态，如果还是未付款就取消订单释放库存。

### 延时只支持18个level原理

为什么只支持18个level?  而不是开放出自定义延时？ 减少Broker排序

延迟时间间隔为：1s、 5s、 10s、 30s、 1m、 2m、 3m、 4m、 5m、 6m、 7m、 8m、 9m、 10m、 20m、 30m、 1h、 2h

```css
https://github.com/apache/rocketmq/issues/336
dongeforever commented on 25 Jun 2018
The delay level is determined by the configuration named 'messageDelayLevel' in broker. So it is not easy to define a enum in the client side.
In fact, I am developing a new evolutional timer message. And It will show in the near future.
```

### 消费方式

#### 集群消费（默认）

一个ConsumerGroup的Consumer实例平均分摊消费生产者发送的消息，某个topic有9条消息，其中一个Consumer Group有三个实例（3个进程或3台机器），每个实例只消费其中3条消息

#### 广播消费

一条消息被多个Consumer消费，即使这些Consumer属于同一个ConsumerGroup，消息也会被每个ConsumerGroup中的每个Consumer消费一次。
