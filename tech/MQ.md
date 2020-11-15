# MQ

## 消息协议

### TCP

 Kafka

### MQTT

Message Queuing Telemetry Transport 消息队列遥测传输。基于TCP/IP，Mosquito、

### AMQP

RabbitMQ

### RTMP





## 为什么要用MQ？

削峰：上游流量大、下游扛不住

解耦：支持业务扩展

冗余：一对多，一个生成者，多个订阅Topic

健壮：消息积压

异步：存队列时不需要立即处理，在需要时取队列数据才处理

消息一致性：利用事务，账号转账如系统A扣钱，系统B加钱

VS：数据库一致性是事务完成，所有数据具有一致状态。

CAP 分区容忍性partition tolerance：数据在不同网络子网，一个子网挂了，其他子网能访问到这个数据，常用保障方法是多个副本复制。

## VS



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

https://www.cnblogs.com/huxi2b/p/6223228.html

LinkIn研发处理流式数据，Kafka一个topic可以分成多个Partition，一个topic可以被多个group消费，**每个Partition只能对应一个消费者消费**，Partition每个消息对应唯一的offset。

### 版本

```css
Kafka 2.10/2.11 不是Kafka的版本，而是编译Kafka的Scala版本
Kafka Server端是Scala编写，Scala主流3个版本分别是2.10、2.11、2.12，Kafka现在每个PULL request都已经自动增加了这三个版本的检查
Kafka广泛使用的版本：0.8.x、0.9.x、0.10.* 
Kafka 0.9.x之前：提供ConsumerConnector、ZookeeperConsumerConnector以及SimpleConsumer，Consumer是Scala编写，包名结构是kafka.consumer.*，分为high-level consumer和low-level consumer 
Kafka 0.9.x开始提供Java版本的Consumer，新版本Consumer可以独立部署，不再需要依赖Server端代码，提供KafkaConsumer和ConsumerRecord，包名结构是o.a.k.clients.consumer.*
```



### 适用场景

收集日志、监控信息、埋点

这部分是较老版本的，待处理整理清楚。  通过Zookeeper维护offset，消费端维护offset，持久化属于日志型持久化默认7天删除消息。

consumer加入group，

```java
@KafkaListener(id="test1",topics = "test-topic", containerFactory="kafkaListenerContainerFactory1")
@KafkaListener(id="test2",topics = "test-topic", containerFactory="kafkaListenerContainerFactory2")
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

![Kafka Ordering Consume](http://hongchengjian.gitee.io/md/img/mq/Kafka%20Ordering%20Comsume.png)

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

![RabbitMQ Model](http://hongchengjian.gitee.io/md/img/mq/RabbitMQ%20Model.png)

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
