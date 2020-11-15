# 云

## 云存储公司

IBM，Pure，NetApp，EMC，SAP

## 云平台

第一梯队：AWS， Azure，GCP，AliYun

第二梯队：vCloud，UCloud，坚果云

## 云虚拟化

 VMware, Hyper-V

## 云原生

云原生：Devops + 持续交付 + 容器化 + 微服务

Cloud+Native 

### AliYun组件

DataWorks

ECS

RDS

CDN

NAT网关

E-MapReduce

Dataphin与阿里云的存储计算引擎Maxcompute、智能图形化分析工具Quick BI结合使用，为数据迁移、治理、规划、可视化及数据应用提供一站式服务。

Teambition 项目管理、进度

DTS

MaxCompute

OSS 文件、图片存储

短信模板

### AWS组件

RDS

Redshift

SQS

EC2

Glue

# 微服务

## DDD

### 实体 Entity

```
实体不是ORM意义上的实体
```

### 值对象 Value Object

```
实体有唯一标识，值对象没有唯一标识
两个实体即便是实体其他所有属性都一样，也被认为是两个不同实体
值对象另一个特征是不可变，所有属性只读，可被安全共享，有复制和共享两种做法
值对象不要让它引用很多其他对象，值对象只是代表一个值
```

### 聚合及聚合根 Aggregate、Aggregate root

```
聚合作用是帮助简化模型对象间的关系
划分聚合是对DDD的进一步深化，会直接映射到程序结构上
每个聚合都有一个聚合根实体，外部访问只能通过聚合根
通常将聚合组织到一个文件夹或一个包，每一个聚集对应一个包，并且每个聚集成员包括 Entity、Value Object、Domain事件、仓储接口、其他工厂对象
```

### 工厂Factories

```
一个单独的工厂通常生产整个聚合，传出聚合根的引用，对外部隐藏了聚合内聚的实现
```

### 仓储Repositories

```
仓储是管理实体的集合
仓储放的对象一定是聚合
domain是以聚合来划边界，聚合要么一起被取出来，要么一起被删除
在领域模型中定义仓储接口，在基础设施层实现具体的仓储
Repositories的实现不是在领域层中
```

### Dao VS  Repositories

```
Dao是细粒度、更接近数据库，Repositories更接近领域，领域对象只依赖Repositories接口
调用链：客户端 ---> 调用领域对象 ---> 领域对象再调Dao ---> 入数据库
```

### Service

```
Service只负责协调并委派业务逻辑给领域对象处理，大部分业务逻辑在领域对象承载和实现
服务对象中通常包含一个动词，Service传入传出参数都应该是DTO
领域服务只有行为没有状态，领域对象有状态和行为，其中状态是指什么？

```

### Domain Event

```
udi dahan http://www.udidahan.com/2009/06/14/domain-events-salvation/
事件：系统事件、应用事件、领域事件
Domain Event的触发点在Domain model中，作用是将领域对象从Repositories或Service中解脱出来，
通过领域事件，实现领域模型对象状态的异步更新、外部系统接口的委托调用，以通过事件派发机制实现系统集成
Domain Event也用表进行存储
```

### DTO

```
Data Transfer Object 以粗粒度数据结构减少网络通信并简化调用接口
```

### Eric  evans 的 n层架构

```css
高层次架构：User Interface ---> Application ---> Domain ---> Infrastructure

User Interface: Facade(为客户端提供粗粒度的调用接口，Facade本身不处理任何的业务逻辑，主要工作是将一个用户请求委托给一个或多个Service进行处理，同时借助Assembler将Service传入或传出的领域对象转化为DTO传输), DTO, Assembler( Assembler 负责DTO和领域对象之间的转换，也可以使用apache common beanutils反射自动实现DTO与领域对象之间相互转换)组件构成，也包括 Web Service, RMI, Rest

Application: 主要组件就是Service，与传统Transaction Script风格的Service一致。但Transaction Script面向过程（复杂业务逻辑都在Service实现，会导致胖服务层，可扩展和可维护性差），Application层的Service面向对象（领域模型具备自己属性行为和状态，领域对象之间通过聚合配合解决实际业务，Servie只负责协调并委托业务）
```

### Domain

```
系统核心层维护面向对象：domain包含entity实体、valueObject值对象、domain event 领域事件、resp
```

## Transaction Script事务脚本模式

```
面向过程方式组织业务，系统一个流程被实现为一个方法，所有方法被组织在一起，放在一个类
取数据 --> 逻辑 --> 数据展示
存数据 ---> 逻辑 --> 保存数据

优点：一个事务不会影响其他事务
缺点：每增加一个业务流程、代码会增加一个或几个方法，业务类中存在大量相似代码，难维护
```



## 基础框架

Spring Cloud，Dubbo，Motan，Sofa

## 协议

Raft VS ZAB VS PAXOS

ZAB是epoch和count双向leader从follower接收数据来生成，Raft是term和index，单向恢复从leader到follower补齐log

## 原则

AKF、无状态、Restful、前后分离、12factor(https://12factor.net/disposability)

## 模式

链式、聚合器、异步消息、数据共享

![Microservice Architecture](http://hongchengjian.gitee.io/md/img/springcloud/Microservice%20Architecture%20VS.png)

## 注解

@RefreshScope 配置变化时，Spring @Bean懒加载初始化配置，rebuilt和依赖重新注入。

### Spring Cloud Commons(扩展核心)

@EnableDiscoveryClient：基本原理：加载META-INF/spring.factories里配置，扩展org.springframework.cloud.client.discovery.EnableDiscoveryClient，源码ref  org.springframework.cloud.client.discovery.EnableDiscoveryClientImportSelector#selectImports。

ServiceRegistry：Auto-Registration，默认是自动注册的,spring.cloud.service-registry.auto-registration.enabled=false可以屏蔽掉自动注册的功能，或者直接@EnableDiscoveryClient(autoRegister=false)单个注册类的屏蔽。Actuator Endpoint，Get /service-registry 拿到注册状态，Post新的注册信息JSON去更新。

Load Balancer Client：ribbon（restTemplate）、SpringWebclient（源码参考 https://github.com/spring-projects/spring-retry）

## 分布式注册中心

Eureka（Netflix），Consul，Nacos，Etcd，Zookeeper

服务之间调用。Eureka高可用Server需相互注册，心跳，一般高可用3台可支撑3000-4000服务。

### Eureka心跳监测配置

```properties
Server服务端
server:
  port: 8761
eureka:
  client:
    #实例是否在eureka服务器上注册自己的信息以提供其他服务发现,默认为true
    register-with-eureka: false
    #此客户端是否获取eureka服务器注册表上的注册信息,默认为true
    fetch-registry: false
  server:
    #开启自我保护模式
    enable-self-preservation: false
    #清理无效节点,默认60*1000毫秒,即60秒
    eviction-interval-timer-in-ms: 5000

Client客户端

spring:
  application:
   name: ek-provider
eureka: 
  instance:
    #eureka客户端需要多长时间发送心跳给eureka服务器，表明他仍然或者，默认30秒
    lease-renewal-interval-in-seconds: 5
    #eureka服务器在接受到实力的最后一次发出的心跳后，需要等待多久才可以将此实力删除
    lease-expiration-duration-in-seconds: 10
    metadata-map: 
      company-name: eureka
  client: 
    #表示eureka client间隔多久去拉取服务器注册信息,默认为30秒
    registry-fetch-interval-seconds: 30
    #表示eureka client间隔多久去拉取服务器注册信息,默认为30秒
    registry-fetch-interval-seconds: 30registry-fetch-interval-seconds: 30
    serviceUrl: 
      defauiltZone: http://localhost:8761/eureka/
logging:
  level: 
    com.netflix: DEBUG
```

Eureka-Server 集群不区分主从节点或者 Primary & Secondary 节点，所有节点相同角色( 也就是没有角色 )，完全对等。

Eureka 支持的状态有 UP, DOWN, OUT_OF_SERVICE, and UNKNOWN。

Eureka自我保护：EMERGENCY! EUREKA MAY BE INCORRECTLY CLAIMING INSTANCES ARE UP WHEN THEY'RE NOT. RENEWALS ARE LESSER THAN THRESHOLD AND HENCE THE INSTANCES ARE NOT BEING EXPIRED JUST TO BE SAFE. 

### 为什么Eureka需自我保护？

Eureka注册服务慢的问题：eureka.instance.leaseRenewalIntervalInSeconds 调整默认的持续时间30s

解决Eureka Server不踢出已关停的节点配置：server端，eureka.server.enable-self-preservation（设为false，关闭自我保护主要）eureka.server.eviction-interval-timer-in-ms     清理间隔（单位毫秒，默认是60*1000）。client端：eureka.client.healthcheck.enabled = true开启健康检查（需要spring-boot-starter-actuator依赖），
eureka.instance.lease-renewal-interval-in-seconds =10		租期更新时间间隔（默认30秒），
eureka.instance.lease-expiration-duration-in-seconds =30  租期到期时间（默认90秒）。

Eureka高可用性：5K-1W实例，3个Eureka Server就可以支撑。AP中的A: 在集群中一部分节点故障后，集群整体是否还能响应客户端的读写请求。

Eureka Prefer IP Address：In some cases, it is preferable for Eureka to advertise the IP addresses of services rather than the hostname. Set eureka.instance.preferIpAddress to true and, when the application registers with eureka, it uses its IP address rather than its hostname.

## 分布式监控中心

CAT(大众点评),SBA,Prometheus(Metrics普罗米修斯，被DigitalOcean或Docker作为基础监控),Grafana,Pinpoint(韩国、非嵌入),谛听(阿里云),Zipkin(Twitter),Appdash(golang),鹰眼(Taobao),StackDriver Trace (Google),云图(蚂蚁),Skywalking-吴晟,Graphite,Statsd,Solarwinds,Zabbix,Centreon,appDynamics,new relic,Kaeger,Overwatch(达达-京东到家618单日订单量400万)

### 分布式调用链

CAT,SkyWalking+RocketBolt,Zipkin,DynaTrace

### 推 VS 拉

Prometheus主动筛选目标，以便从中检索指标；InfluxDB是直接推数据。

Time Series Database 时间序列数据库InfluxDB 

Prometheus向其目标发起查询，则整个配置在Prometheus服务器端完成，而不是在各个目标上完成。Prometheus决定取值，以及取值的频率。

推VS拉

集中 VS 广播

定时 VS 实时

消费能力

拉Pull：集中控制，定时轮询。能够实现速率控制(针对个性化需求强，针对不同目标实现不同速率)，按频率采样牺牲了实时性，采样数据需考虑消费能力。无效的Pull也消耗性能。需协调机制(Zookeeper)在不同客户端之间做分配，对服务端压力很轻(服务端仅需对客户端查询做出响应)。

推Push（广播方式）：可能会导致向目标发送过多数据的风险，会使目标崩溃。一收到数据可以立即推给目标，实时性很好。推多个目标需保存push状态，状态转移到数据库减轻服务器压力。有失败有成功。不能确保发送成功，即使发送成功，也不能保证目标是否接收成功。要求目标有很强消费能力。

守城门是拉不是推？若是推，攻打门口堆满石头困死守城人。

### Skywalking-吴晟  chéng VS Pinpoint-韩国

都是字节码注入（所以无侵入），但Skywalking兼容OpenTracing、协议是gRPC、发布包Jar

Pinpoint协议是Thrift，发布包是War

### Metrics

系统度量监控

#### 5种基本度量

```css
Gauges：计量器 		特点：可增减 		场景：温度、内存使用量
Counters：计数器 	特点：单调递增     场景：服务请求数、任务完成数、错误出现次数
Histograms：直方图	度量流数据中value的分布情况，计算最大/小值、平均值，方差，分位数（如中位数，或者95th分位数）
Timers：计时器		特点：只能自增		 场景：平均每秒请求数、最近1分钟平均每秒请求数、最近5分钟平均每秒请求数
Meters：TPS计数器	某段代码执行的耗时的统计及计算 	场景：请求时延、磁盘读时延
```

### Tracing

```
Spring Cloud Sleuth在Zuul对于每个请求生成一个日志id后，通过Http header方式将id带到不同的服务应用中。单体应用通过sl4j或logback实施日志跟踪。Sleuth在某些业务场景如日志中添加请求时间、监控每条日志的客户ip等需要进行功能扩展。
```



## 分布式日志系统  Logging

ELK(Kibana,ElasticSearch,Logstash),Kafka,Flume,Splunk,Filebeat（比Flume轻量级）

## 分布式配置中心

Apollo,Nacos,DisConf,Spring Cloud Config

## 分布式网关

F5,Ngnix +（打通Consul）,ESB,Kong,Gateway,Zuul,Soul

Netflix ZuulFilter基于Servlet（pre、router、post）

SpringCloud gateway基于Spring5，支持websocket，GatewayFilter、GlobalFilter

## 分布式事务

Seata(GIT Fescar),dts,tcc-transaction,hmily,ByteTCC,myth,EasyTransaction,tx-lcn

二阶段提交2PC、三阶段提交3PC、Sagas长事务、补偿事务、可靠事件模式(本地事件表、外部事件表)、可靠事件模式(非事务消息、事务消息)、TCC

Seata支持AT、TCC、XA、Saga

![Distributed Transaction](http://hongchengjian.gitee.io/md/img/db/Distributed%20Transaction%20VS.png)

### Seata AT  Simple Extensible Autonomous Transaction Architecture（侵入业务最小，但是性能没TCC高，TCC需写代码来处理问题比较多）

http://seata.io/zh-cn/docs/overview/what-is-seata.html 

```
Seata AT并发、批量都超级消耗性能，耗在：云做GLOBAL，做BRANCH表的来来回读写，还要对UNDO表做读写，还要在注册中心间消息来回

A 账户服务 B 订单服务 C 其他服务 。 B调用A时 B发生错误 A会回滚 但此时B还未到发送错误的代码 C就调用A了，B发生错误了 这时A就不会回滚了吧 导致余额有偏差。对批量的数据是单条加锁的，极慢。
 
TCC缺陷：
```



```css
Seata AT(包含Server、Client)使用
1.Server
Server支持：直接部署，Docker, 使用 Docker-Compose, 使用 Kubernetes, 使用 Helm
https://github.com/seata/seata/releases 下载 v1.3.0 开箱即用
Linux/Mac $ sh ./bin/seata-server.sh
Windows bin\seata-server.bat
2.Client
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-alibaba-seata</artifactId>
    <version>2.1.0.RELEASE</version>
</dependency>
<dependency>
    <groupId>io.seata</groupId>
    <artifactId>seata-all</artifactId>
    <version>1.3.0</version>
</dependency>

# AT模式 一个库需要建一个对应的undo_log表，undo_log表数据回滚后会清掉
-- for AT mode you must to init this sql for you business database. the seata server not need it.
CREATE TABLE IF NOT EXISTS `undo_log`
(
    `branch_id`     BIGINT(20)   NOT NULL COMMENT 'branch transaction id',
    `xid`           VARCHAR(100) NOT NULL COMMENT 'global transaction id',
    `context`       VARCHAR(128) NOT NULL COMMENT 'undo_log context,such as serialization',
    `rollback_info` LONGBLOB     NOT NULL COMMENT 'rollback info',
    `log_status`    INT(11)      NOT NULL COMMENT '0:normal status,1:defense status',
    `log_created`   DATETIME(6)  NOT NULL COMMENT 'create datetime',
    `log_modified`  DATETIME(6)  NOT NULL COMMENT 'modify datetime',
    UNIQUE KEY `ux_undo_log` (`xid`, `branch_id`)
) ENGINE = InnoDB
  AUTO_INCREMENT = 1
  DEFAULT CHARSET = utf8 COMMENT ='AT transaction mode undo table';

在项目启动类加上@EnableAutoDataSourceProxy注解，允许数据库代理。(注意(1)引包不要和SpringBoot @Transaction的事务管理器冲突，如果回滚的数据被其他事务已修改，Seata XA是不能回滚的，会报错(2)如果@GlobalTransactional Service执行超时等待，超过了Seata可接受的最大延迟时间，会抛异常(不能回滚的原因是不能写入undo_log)，Seata会执行默认的熔断策略，认为服务不可用，过一段时间后打开)

在需要发起分布式事务的地方加上@GlobalTransactional(@GlobalTransactional注在Service层，能注在Controller层？未测)

启动项目加上 --seataEnv=dev指定seata的环境，区分不同的配置。

```

部署Server支持的启动参数

```bash
# man ref http://seata.io/zh-cn/docs/user/configurations.html
$ sh ./bin/seata-server.sh -p 8091 -h 127.0.0.1 -m file
```





## 分布式定时任务调度和管理

Elastic Job,XXL-Job

### XXL-Job

![img](https://img2018.cnblogs.com/blog/753271/201909/753271-20190924135844231-171876118.png)

关注调度中心和执行器

找到入口com.xxl.job.admin.core.conf.XxlJobAdminConfig调度中心端的配置数据

JDK中的Timer类

cron无页面暂停、

### 设计一个调度中心要素

```css
讲故事
Job、task：sendMail、copyData
Trigger
Scheduler(协调、管理Job、算法)
持久化(任务挂掉、任务执行一半中断):内存、数据库存储  DriverDelegate代理屏蔽数据库细节
UI界面管理
数据库的‘行’锁嘛, 比如SELECT * FROM LOCKS where LOCK_NAME='TRIGGER' FOR UPDATE ，就把那一行记录给锁住了，别的事务只能等待当前事务commit以后才能访问
https://www.cnblogs.com/peke/p/9212351.html
```



```java
XxlJobAdminConfig implements InitializingBean, DisposableBean
```

```java
InitializingBean	
    @Override	
    public void afterPropertiesSet() throws Exception {
    
	}

DisposableBean		
    @Override	
    public void destroy() throws Exception {
    
	}
```

```java
 public void init() throws Exception {
        // init i18n
        initI18n();

        // admin registry monitor run
        JobRegistryMonitorHelper.getInstance().start();

        // admin fail-monitor run
        JobFailMonitorHelper.getInstance().start();

        // admin lose-monitor run
        JobLosedMonitorHelper.getInstance().start();

        // admin trigger pool start
        JobTriggerPoolHelper.toStart();

        // admin log report start
        JobLogReportHelper.getInstance().start();

        // start-schedule
        JobScheduleHelper.getInstance().start();

        logger.info(">>>>>>>>> init xxl-job admin success.");
    }
```

思考后台Daemon线程 VS 守护线程

```
Daemon主程序运行时在后台提供一种通用服务的线程
```



```java
public class JobScheduleHelper{
    private volatile boolean scheduleThreadToStop = false;
	private Thread scheduleThread;
    private Thread ringThread;
	public void start(){
        // 后台线程1
 	 	scheduleThread = new Thread(new Runnable() {
             @Override
            public void run() {
                 // 思考：如何设计一个接收信号停止运行新的线程？在跑的线程或在等待的线程如何处理？
                  while (!scheduleThreadToStop) {
                      
                  }
            }
         });
        scheduleThread.setDaemon(true);
        scheduleThread.setName("...");
        scheduleThread.start(); 
                                    
		// 后台线程2
		ringThread = new Thread(new Runnable() {
            @Override
            public void run() {

            }
        });
                             
 	 }
                                    
                                    
	 public void toStop(){
         // 给一个信号目的关闭线程
       	 scheduleThreadToStop = true;
     }
}
                                    
  
VS

public class JobScheduleHelper extends Thread {
    @Override
    public void run() {

    }
}        
                                
```



（1）悲观全表锁锁住获取任务资格 select * from xxl_job_lock where lock_name = 'schedule_lock' for update;

当开启一个事务进行for update时候，另一个事务也有for update会一直等到第一个事务结束

可扩展成悲观单行锁 或 redis分布式锁？

（2) 获取未来 #{PRE_READ_MS} 秒即将执行的任务

```sql
SELECT t.id,
		t.job_group,
		t.job_cron,
		t.job_desc,
		t.add_time,
		t.update_time,
		t.author,
		t.alarm_email,
		t.executor_route_strategy,
		t.executor_handler,
		t.executor_param,
		t.executor_block_strategy,
		t.executor_timeout,
		t.executor_fail_retry_count,
		t.glue_type,
		t.glue_source,
		t.glue_remark,
		t.glue_updatetime,
		t.child_jobid,
		t.trigger_status,
		t.trigger_last_time,
		t.trigger_next_time
		FROM xxl_job_info AS t
		WHERE t.trigger_status = 1
			and t.trigger_next_time <![CDATA[ <= ]]> #{maxNextTime}
		ORDER BY id ASC
		LIMIT #{pagesize}
```

（3）遍历scheduleList

## 分布式限流熔断降级

Sentinel,Redis,Guava,Hystrix

### 限流

#### Scenario

稀缺资源（秒杀、抢购）、写服务（评论、下单）、频繁复杂查询（评论最后几页）不能用缓存和降级来解决，需限流来限制并发、请求量

限流有：限制数据库连接池、线程池、nginx limit_conn限制瞬时并发连接数、限制时间窗口的平均速率（Guava RateLimiter、Nginx limit_req）、限制远程接口调用速率、限制MQ消费速率、网络连接数、网络流量、CPU、内存

#### 应用级限流

Tomcat Connector参数：acceptCount、maxThreads。

MySQL：max_connections

Redis: tcp_backlog

#### 细粒度

Lua+Nginx+Redis：一致性hash将分布式限流

#### Redis限流

每分钟某个用户访问服务接口数不超过阀值n次，set key exprireTime = 60s，每访问一次就incre key做+1。 

#### Token Bucket 令牌桶

设置参数 令牌桶添加速率r，令牌桶最大容量N 

Ex. Guava RateLimiter

#### Leaky Bucket 漏桶

Ex.  Guava SmoothWarmingUp

#### Fix Window Counter 固定窗口计数

两个计数参数，计数周期T及最大访问调用数N，缺陷是周期切换时，突破限流最大数N

#### Sliding Window Counter 滑动窗口计数

优化了Fix Window Counter算法的周期切换问题

### 熔断

#### Scenario

#### 超时、链路中断CircuitBreaker、雪崩、超过失败阀值

#### Sentinel VS Hystrix

关注点：Hystrix关注熔断和隔离，资源定义与规则配置强耦合，线程池隔离针对不同服务不同线程池，信号量隔离限制并发数，缺点是无法对慢应用自动降级，只能等待客户端自己超时(存在级联阻塞)；Sentinel 关注流量控制、方法/代码。Sentinel和Hystrix熔断降级本质是熔断器模式Circuit Breaker Pattern，都支持基于失败比率(异常比率)熔断降级，Sentinel还支持平均响应时间的熔断降级(**防止调用非常慢造成级联阻塞**)。Hystrix 1.5之前基于环形数组实现滑动窗口，通过锁配合CAS操作对每个桶的统计信息进行更新。Hystrix 1.5重构将指标统计数据结构抽象成**响应式流**reactive stream底层改造成了基于 RxJava 的事件驱动模式，在服务调用成功/失败/超时的时候发布相应的事件，通过一系列的变换和聚合最终得到实时的指标统计数据流，可以被熔断器或 Dashboard 消费。**Sentinel**抽象出**Metric 指标****统计接口，实现是基于 `LeapArray` 滑动窗口。Sentinel-core没任何多余依赖，打包不到200KB，够轻量。Sentinel单机超25WQPS性能损耗影响5% - 10%，损耗够小。

|    比较点    |           Hystrix            |                   Sentinel                   |
| :----------: | :--------------------------: | :------------------------------------------: |
|   隔离策略   |    线程池隔离或信号量隔离    |                  信号量隔离                  |
|   熔断降级   |         基于失败比率         |            基于响应时间或失败比率            |
| 实时指标实现 |        RxJava滑动窗口        |              LeapArray滑动窗口               |
|   规则配置   |        支持多种数据源        |                支持多种数据源                |
|    扩展性    |             插件             |                  多个扩展点                  |
|   基于注解   |             支持             |                     支持                     |
|     限流     |            不支持            |        基于QPS，支持基于调用关系限流         |
|   流量整形   |            不支持            |            支持慢启动、均匀器模式            |
| 系统负载保护 |            不支持            |                     支持                     |
|    控制台    |            不完善            | 可配置规则、开箱即用、查看秒级监控、机器发现 |
| 常见框架适配 | Servlet,Spring Cloud Netflix |       Servlet,Spring Cloud,Dubbo,gRPC        |

Hystrix命令模式实现，对外部资源的调用和fallback(熔断反馈fallback：hystrix.command.default.fallback.enabled)封装成一个命令对象(extends HystrixCommand  HystrixObservableCommand)，底层基于RxJava。每个 Command 创建时都要指定 commandKey 和 groupKey（用于区分资源）以及对应的隔离策略（线程池隔离 or 信号量隔离，执行策略isolation.strategy：hystrix.command.default.execution.isolation.strategy=THREAD）。线程池隔离模式下需要配置线程池对应的参数（线程池名称、容量、排队超时等），然后 Command 就会在指定的线程池按照指定的容错策略执行；信号量隔离模式下需要配置最大并发数，执行 Command 时 Hystrix 就会限制其并发调用。

Sentinel 资源定义与规则配置耦合度更低，Hystrix  Command 强依赖于隔离规则，原因是隔离规则会直接影响 Command 执行， Hystrix 会解析 Command 隔离规则来创建 RxJava Scheduler 调度执行，若是线程池模式则 Scheduler 底层的线程池为配置的线程池，若是信号量模式则简单包装成当前线程执行的 Scheduler。**而Sentinel则不一样，开发的时候只需要考虑这个方法/代码是否需要保护，可以动态实时修改。**Sentinel 从 0.1.1 版本开始支持基于注解的资源定义方式，可以通过注解参数指定异常处理函数和 fallback 函数。Sentinel 提供多样化的规则配置方式。除了直接通过 `loadRules` API 将规则注册到内存态之外，用户还可以注册各种外部数据源来提供动态的规则。用户可以根据系统当前的实时情况去动态地变更规则配置，数据源会将变更推送至 Sentinel 并即时生效。

Hystrix Dashboard 监控单个，Turbine(Hystrix Dashboard)升级， 断路器聚合监控(整个系统)。

### 降级

#### Scenario

RPC访问本地伪装或非真实Mock的服务

## 分布式服务权限控制系统

OAuth,JWT,SSO,Shiro,Security

## 分布式服务和系统诊断

Arthas

## 分布式流程和服务编排

Coroutine,Akka,Kilim,Flowable,Axon

## 分布式锁

ZK(Curator),Redis(Redisson),DB建表增删

## 加锁对象

对同一资源（资源可以是单条、多条数据，也可以是一段操作），优先考虑对单条或数据分片加分布式锁，对批量数据操作加锁慢

## 场景

分布式多实例、滤重(防重复执行，如定时任务、高并发插入)

## Redis

set(key, value, expireTime);

## ZooKeeper

注册增加一个节点加锁、删掉一个节点解锁

## 数据库

建表，插入和删除做分布式锁

## Redis分布式锁问题

### （1）锁未被释放

情况一：加锁—>处理完业务—> 未释放锁导致其他线程一直尝试获取锁阻塞抛异常

```java
redis.clients.jedis.exceptions.JedisConnectionException: Could not get a resource from the pool 
```

```java
 public String stockLock() {
        RLock lock = redissonClient.getLock("stockLock");
        try {
            /**
             * 获取锁
             */
            if (lock.tryLock(10, TimeUnit.SECONDS)) {
              
                /**
                 * 扣减库存
                 */
                。。。。。。
            } else {
                LOGGER.info("未获取到锁业务结束..");
            }
        } catch (Exception e) {
            LOGGER.info("处理异常", e);
        } 
        return "ok";
  }
代码问题：（1）锁的key没统一管理（2）锁没有释放导致线程池打满引发服务大面积瘫痪（3）日志级别
```

情况二：redis线程池无空闲线程处理客户端命令

redis线程池：核心线程数--->阻塞队列--->最大线程数--->线程池拒绝

jedis线程池配置：

```xml
	 # redis连接池配置少影响TPS上不去，导致很多线程等待Redis线程池
	 <property name="maxActive" value="20" />
   <property name="maxIdle" value="3" />
   <property name="maxWait" value="15000" />
   <property name="timeBetweenEvictionRunsMillis" value="60000" />
   <property name="minEvictableIdleTimeMillis" value="180000" />
```



```java
public void lock() { 
  // for比while效率高，for的指令集更少
      for(;;;) { 
          boolean flag = this.getLock(key); 
          if (flag) { 
                TODO ......... 
          } else { 
                // 释放当前redis连接 
                redis.close(); 
                // 休眠1000毫秒, 拿到锁的线程处理完业务及时释放锁，如果是重入锁未拿到锁后，线程可以释放当前连接并且sleep一段时间 
                sleep(1000); 
          } 
        } 
    } 
```

### （2）B的锁被A释放

SETNX 加锁后，业务逻辑耗时已超过Redis锁过期时间，线程A的锁自动释放（删除key），B线程检测到key不存在，执行SETNX拿到锁，但是线程A执行完业务逻辑还是会释放key，导致B线程的锁被A释放了

解决思路：比较线程id和唯一线程相关的key标识、必须等线程A执行任务逻辑完才释放锁，任务逻辑未执行完进行续约过期时间expireTime

### （3）获取锁等待的时间远超过数据库事务超时时间

事务自动提交的情况下会有超时限制，key长时间获取不到锁，获取锁等待的时间远超过数据库事务超时时间，程序会抛异常

```java
@Transaction 
   public void lock() { 
 
        while (true) { 
            boolean flag = this.getLock(key); 
            if (flag) { 
                insert(); 
            } 
        } 
    } 
```

解决方案：将数据库事务改为手动提交、回滚事务

```java
@Autowired 
    DataSourceTransactionManager dataSourceTransactionManager; 
 
    @Transaction 
    public void lock() { 
        //手动开启事务 
        TransactionStatus transactionStatus = dataSourceTransactionManager.getTransaction(transactionDefinition); 
        try { 
            while (true) { 
                boolean flag = this.getLock(key); 
                if (flag) { 
                    insert(); 
                    //手动提交事务 
                    dataSourceTransactionManager.commit(transactionStatus); 
                } 
            } 
        } catch (Exception e) { 
            //手动回滚事务 
            dataSourceTransactionManager.rollback(transactionStatus); 
        } 
    } 
```

回滚事务发生的情况：

(1)执行SQL的connection与开启事务的connection必须是同一个才能对事务进行控制，事务Catch RuntimeException才回滚

(2)手动提交时在异常处理机制需手动回滚

### （4）锁过期expire时间续约

锁过期expire时间比执行完任务时间要长，redisson(加锁、解锁、续约)看门狗WatchDog在加锁后会注册一个定时任务监听锁，检查周期是：加锁失效时间的1/3，如加锁3s释放，检查是1s一次，加锁业务没执行完，会自动续期重置为加锁失效时间3s。requestId可以是当前线程id也可以唯一标识业务处理的id

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

（4）redis主从master-slave  A选择一台master加锁key成功后，master将key异步复制给slave，若master宕机进行主备切换， B在新master加锁成功了，导致同一时刻多请求加锁成功，如何防止？



## 分布式压测平台

JMeter,LoadRunner,Ab

## 分布式全局主键系统

Redis,Zookeeper,Twitter Snowflake

### 主键思考点

快(占CPU高?）、是否有序?(排序需求)、占用空间(位数是否够用?)、随机?、是否独立模块?(穿插不同业务线)、是否预生成、是否有池子、获取是否批量、单个是否自增、是否唯一（MD5、SHA、SM3 etc）、是否对业务友好(不同业务用不同位数标识分开、利于区分)、是否纯数字、字符串

```css
(1)MySQL自增  Q：OrderId直接做主键的缺陷？
(2)系统生成 snowfake、美团(Leaf)、滴滴(Tinyid)、百度(uid-generator)、redis incre
(3)Oracle sequence + 触发器函数
(4)UUID
(5)SHA、MD5、SM3、RSA
```

比如在插入表前，重点是前，对于涉及很多张表（可能一个模块几张表）都依赖于这个操作。缺陷排序、递增、索引效率str < 数值

中间表需要id吗？需要，即使没有业务含义也需要id

innodb必须要id吗？默认的id是int型，一般设计id是long型，防溢出。

MySQL innodb情况下，中间表为什么要创建主键？

https://blog.jcole.us/2013/05/02/how-does-innodb-behave-without-a-primary-key/

如果表中没有主键或者一个合适的的唯一索引，InnoDB内部会以一个包含行ID值的合成列生成一个隐藏的聚簇索引。表中的行是按照InnoDB分配的ID排序的。行ID是一个6字节的字段，随着一个新行的插入单调增加。因此，行ID顺序物理上是插入顺序。



## 分布式自动化测试分布式自动化API文档

Swagger,YAPI

## 分布式分库分表中间件

[当当Sharding-JDBC(多数据源Sharding Sphere)]( https://github.com/apache/incubator-shardingsphere),[蘑菇街TSharding]( https://github.com/baihui212/tsharding),[sharding](https://github.com/go-pg/sharding),[淘宝TDDL](https://github.com/alibaba/tb_tddl),[360 Atlas](https://github.com/Qihoo360/Atlas),[阿里巴巴B2B Cobar](https://github.com/alibaba/cobar),[美团MyCAT基于Cobar](http://www.mycat.org.cn/),[58同城 Oceanus](https://github.com/58code/Oceanus),[OneProxy支付宝楼方鑫](http://www.cnblogs.com/youge-OneSQL/articles/4208583.html),[谷歌Vitess](https://github.com/youtube/vitess)

```
Sharding-JDBC 比较常用，无中心化，适合轻量级OLTP
分片算法支持通过=、BETWEEN和IN分片，
只提供分片策略需开发者自行实现分片算法，提供了四种
PreciseShardingAlgorithm 精确分片适合单一键作为分片键的=与IN场景 
RangeShardingAlgorithm + StandardShardingStrategy 范围分片适合单一键作为分片键的BETWEEN AND场景
ComplexKeysShardingAlgorithm + ComplexShardingStrategy 复合分片适合多键作为分片键，复杂
HintShardingAlgorithm + HintShardingStrategy 
```

### 分库分表

```css
分库缓单库的session和连接池压力
分表缓单表数据量大压力，但并没有缓库本身压力
```

#### 切分模式

##### 水平切分

同一个表拆不同库，按数据行划分，有分表分库两种模式

##### 垂直切分

不同表分不同库，专库专用

按业务专库专用切分，业务之间join用接口替代

#### 分库分表策略

```css
id取模、核心重要程度、id或字段数值、日期范围(冷数据)、热数据呢？
分表策略：
(1)PK range 1~10000，10001~20000；一月份，二月份（缺陷按月份出现某月暴增，查询带时间） 适合归档处理 Ex.拉最近三个月订单
(2)hash + mod  hash%2的n次方  Ex.某个用户想查询他产生的所有订单
(3)range + hash

Ex. 库有256 个，每个库中有1024个表，PK＝262145
1.中间变量　＝ PK % (库数量 * 每个库的表数量)			262145 %（256*1024）= 1;
2.库序号　＝　取整(中间变量 / 每个库的表数量)	 		 取整（1／1024）= 0;
3.表序号　＝　中间变量 % 每个库的表数量;				  1 % 1024 = 1;
PK = 262145，将被路由到第0个库的第1个表
```

#### 分表分库影响

（1）原有业务的报表和分页(对业务影响最小的数据迁移烦)

```
报表：数据量小，遍历N张分表，依赖Java多线程并发查询分表数据然后汇总
数据量大，上大数据平台，历史数据归档将N个月之前的数据迁移到HBASE，保证关系型数据库数据在瓶颈之下

原有的分页查询不能再用了，只能提供按分表字段的查询，Ex.订单id分表，查询条件必须带上订单id，不然就遍历N张分表
```

（2）跨节点聚合和跨节点join 

```java
Ex.操作数据前做路由判断：
新数据写入分表查也走分表；
老数据走历史数据，操作还是走旧表；
新数据产生足够多时，几乎所有操作都是针对分表，启动数据迁移；
数据迁移完，去掉路由判断；
```

（3）分布式事务

## 分布式消息队列中间件

RocketMQ,Kafka,ActiveMQ,Tibco,RabbitMQ

## 分布式缓存

Redis, MongoDB,Aerospike

## 分布式数据库分析诊断系统

慢SQL,听云

## 分布式自动化数据库脚本升级

Flyway

## 运维发布

DevOps,CICD和Pipeline,容器(Docker)化,K8S, Jenkins,蓝鲸,TriAquae,Choerodon（猪齿鱼）,Ansible,Artifactory,Terraform(Go),Pulumi

# Spring

## SpringMVC执行流程

![SpringMVC1](http://hongchengjian.gitee.io/md/img/springmvc/SpringMVC1.png)

![SpringMVC2](http://hongchengjian.gitee.io/md/img/springmvc/SpringMVC2.png)

## IOC容器的生命周期

![IOC](http://hongchengjian.gitee.io/md/img/spring/IOC.png)

扩展点

```java
  BeanPostProcessor
  InstantiationAwareBeanPostProcessor
  BeanNameAware
  ApplicationContextAware
  BeanFactoryAware
  BeanFactoryPostProcessor
  InitializingBean
  DisposableBean
  ApplicationListener
  ApplicationContextInitializer
  FactoryBean
  CommandLineRunner
  @org.springframework.core.annotation.Order进行标注或者实现org.springframework.core.Ordered
```

## AOP

### AOP原理

代理

静态代理：编译时确定了被代理类

动态代理（RPC、AOP）：运行时确定了被代理类

RPC不能提前知道各个业务方要调哪些接口的哪些方法，动态代理建立一个Proxy给客户端使用，方便框架搭建逻辑。

### AOP可以切final方法？不能



### AOP不能切Private方法原理？

```java
public class Enhancer extends AbstractClassGenerator {
	public class VisibilityPredicate implements Predicate {
        public boolean evaluate(Object arg) {
            Member member = (Member)arg;
            int mod = member.getModifiers();
            //  关键代码
            if (Modifier.isPrivate(mod)) {
                return false;
            } else if (Modifier.isPublic(mod)) {
                return true;
            } else if (Modifier.isProtected(mod) && this.protectedOk) {
                return true;
            } else {
                return this.samePackageOk && this.pkg.equals(TypeUtils.getPackageName(Type.getType(member.getDeclaringClass())));
            }
    }
}
SubClass
CGlib继承(要被动态代理的类 == 类作为父类)，重写父类的方法。SubClass不可以@Overwrite Parent Class的private 方法，但SubClass可以实现一个与ParentClass同名的方法，既不是@Overwrite也不是@Overload。SubClass不可以@Overwrite Parent Class的final方法。
```

### 动态代理两种实现方式适用场景？

JDK静态代理：写一个代理类只服务一个类的代理操作，若需要代理的类很多要写很多代理类，崩溃。

JDK动态代理：Proxy、InvocationHandler，面向接口

JDK动态代理会代理对象中的所有方法，对于Object中继承的方法，会代理toString方法，但是不会代理equals，hashCode，getClass方法。 

原因：在Spring中的JdkDynamicAopProxy类的invoke方法执行时会判断

```java
      if ((!this.equalsDefined) && (AopUtils.isEqualsMethod(method)))
      {
        return Boolean.valueOf(equals(args[0]));
      }
      if ((!this.hashCodeDefined) && (AopUtils.isHashCodeMethod(method)))
      {
        return Integer.valueOf(hashCode());
      }
      if ((!this.advised.opaque) && (method.getDeclaringClass().isInterface()) && 
        (method
        .getDeclaringClass().isAssignableFrom(Advised.class)))
      {
        return AopUtils.invokeJoinpointUsingReflection(this.advised, method, args);
      }
```

CGLib：Code Generation Library 因创建对象花费时间多，适合singleton代理对象或具有实例池的代理

AOP是不侵入代码做增强功能，切点可以切注解也可以切方法，Spring AOP默认配置：JDK动态代理，SpringBoot AOP默认是Cglib。

## Rest服务

Rest uri对资源访问，方法分别对应增删查改：GET查幂等、PUT改，非幂等、POST增，非幂等、DELETE删幂等

### GrapHQL VS Rest

GrapHQL是API定义语法或者框架，仅有语法定义，并没有限制实现的语言。语法分两类Query接口用来获取数据，Mutation接口用来更新数据。

GrapHQL更灵活，安全控制难，监控不友好。实现版有Python的django、flask和golang。

## Rest增删查改注解

@GetMapping("/{id:\\d+}")（配置表id是code，而业务实体时：id是数据库主键id，非业务实体id）、@RequestMapping("/user")、@PostMapping、@PutMapping、  @DeleteMapping("/{id:\\d+}")

@RestController

### 方法传参注解

@PathVariable、@RequestBody

### 返回json处理注解

Jackson的@JsonView 使用 https://blog.csdn.net/qq_37659167/article/details/82960556

### JUnit常用注解

@Before 在执行测试方法前先执行其标注的方法

### 兼容老Spring项目注解

@ImportResource导入老的Spring项目配置文件

## Spring VS SpringBoot VS SpringMVC

Spring核心IOC、AOP。

SpringAware 感知bean根据id去IOC容器里去bean对应的属性。

Aware、Filter、Handler三个组件的区别？

一次浏览器请求处理过程？

IOC： Inversion控制是IOC控制了对象，不再是主动new 。反转是由容器来帮忙创建及注入依赖对象、接口的具体实现。Container容器本质是集合map。

AOP： @Aspect、@Pointcut（可以切自定义注解，也可以切方法）、@Before、@After、@Around

如何切自定义注解，demo项目？

注意AOP为啥不能代理private方法，只能代理public方法？确认bean 是AopProxy代理的对象，如何确认？三种方式

若public方法调了private方法，可以代理吗？

```java
AopUtils.isAopProxy()
AopUtils.isCglibProxy() //cglib
AopUtils.isJdkDynamicProxy() //jdk动态代理
```

注意context:component-scan 重复扫描（bean实例化多次）影响事务。

注意基于类的代理而非接口，若代理父类 execution(* com.XXX.service..*+.*(..))。

```css
-execution * com.yl.spring.aop.ArithmeticCalculator.*(..):匹配ArithmeticCalculator中声明的所有方法，第一个*代表任意修饰符及任意返回值，第二个*代表任意方法，..匹配任意数量的参数。若目标类与接口与切面在同一个包中，可以省略包名。
-execution public * ArithmeticCalculator.*(..):匹配ArithmeticCalculator接口的所有公有方法
-execution public double ArithmeticCalculator.*(..):匹配ArithmeticCalculator中返回double类型数值的方法
-execution public double ArithmeticCalculator.*(double, ..):匹配第一个参数为double类型的方法，..匹配任意数量任意类型的参数
-execution public double ArithmeticCalculator.*(double, double):匹配参数类型为double，double类型的方法
```

SpringMVC是基于Servlet，属于Spring Web层开发一部分。

SpringBoot Outofbox开箱即用和默认优于配置Convention over configuration。专注于开发后端接口，不专注于开发前端视图，注解插件配置简化了xml配置流程，方便很快地开发单个微服务。SpringBoot打包和分发依赖Maven和Gradle，maven VS gradle：maven是扫整个pom下的类字节码，扫到一个就用这个，会duplicate class错误，并不会比较相同类字节码的版本。而gradle是扫整个，遇到相同的会比较版本后选择用高版本。SpringBoot是Starter插件形式维护模块，提供parent pom管理。SpringBoot的CLI 命令行界面 和 GVM Groovy环境管理器处理版本的安装和管理。

SpringCloud更注重全局微服务的治理、整合，全家桶管理多个SpringBoot单体服务。

## 底层细节

@Order如何保证有序的底层？

注解反射获取注入bean，Comparator比较注解int值排好序后，将bean加入LinkedHashSet，

@Order、Ordered不影响类的加载顺序而是影响Bean加载如IOC容器之后执行的顺序（优先级）

```java
@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.TYPE, ElementType.METHOD, ElementType.FIELD})
@Documented
public @interface Order {
	/**
	 * 默认是最低优先级,值越小优先级越高, @Order()值从0开始
	 */
	int value() default Ordered.LOWEST_PRECEDENCE;
}

public interface Ordered {
    int HIGHEST_PRECEDENCE = -2147483648;
    int LOWEST_PRECEDENCE = 2147483647;
    int getOrder();
}

public ConfigurableApplicationContext run(String... args) {
        StopWatch stopWatch = new StopWatch();
        stopWatch.start();
        ConfigurableApplicationContext context = null;
        Collection<SpringBootExceptionReporter> exceptionReporters = new ArrayList();
        this.configureHeadlessProperty();
        SpringApplicationRunListeners listeners = this.getRunListeners(args);
        listeners.starting();

        Collection exceptionReporters;
        try {
            ApplicationArguments applicationArguments = new DefaultApplicationArguments(args);
            ConfigurableEnvironment environment = this.prepareEnvironment(listeners, applicationArguments);
            this.configureIgnoreBeanInfo(environment);
            Banner printedBanner = this.printBanner(environment);
            context = this.createApplicationContext();
            exceptionReporters = this.getSpringFactoriesInstances(SpringBootExceptionReporter.class, new Class[]{ConfigurableApplicationContext.class}, context);
            this.prepareContext(context, environment, listeners, applicationArguments, printedBanner);
            this.refreshContext(context);
            this.afterRefresh(context, applicationArguments);
            stopWatch.stop();
            if (this.logStartupInfo) {
                (new StartupInfoLogger(this.mainApplicationClass)).logStarted(this.getApplicationLog(), stopWatch);
            }

            listeners.started(context);
            //这里是重点，调用具体的执行方法
            this.callRunners(context, applicationArguments);
        } catch (Throwable var10) {
            this.handleRunFailure(context, var10, exceptionReporters, listeners);
            throw new IllegalStateException(var10);
        }

        try {
            listeners.running(context);
            return context;
        } catch (Throwable var9) {
            this.handleRunFailure(context, var9, exceptionReporters, (SpringApplicationRunListeners)null);
            throw new IllegalStateException(var9);
        }
    }

   private void callRunners(ApplicationContext context, ApplicationArguments args) {
        List<Object> runners = new ArrayList();
        runners.addAll(context.getBeansOfType(ApplicationRunner.class).values());
        runners.addAll(context.getBeansOfType(CommandLineRunner.class).values());
        //重点来了，按照定义的优先级顺序排序
        AnnotationAwareOrderComparator.sort(runners);
        Iterator var4 = (new LinkedHashSet(runners)).iterator();
        //循环调用具体方法
        while(var4.hasNext()) {
            Object runner = var4.next();
            if (runner instanceof ApplicationRunner) {
                this.callRunner((ApplicationRunner)runner, args);
            }

            if (runner instanceof CommandLineRunner) {
                this.callRunner((CommandLineRunner)runner, args);
            }
        }

    }

    private void callRunner(ApplicationRunner runner, ApplicationArguments args) {
        try {
            //执行方法
            runner.run(args);
        } catch (Exception var4) {
            throw new IllegalStateException("Failed to execute ApplicationRunner", var4);
        }
    }

    private void callRunner(CommandLineRunner runner, ApplicationArguments args) {
        try {
            //执行方法
            runner.run(args.getSourceArgs());
        } catch (Exception var4) {
            throw new IllegalStateException("Failed to execute CommandLineRunner", var4);
        }
    }
```



# SpringBoot

## SpringBoot Servlet容器

```java
public class XXXServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {        

    //TODO Auto-generated method stub super.doGet(req, resp);

    }
}

@SpringBootApplication
@ServletComponentScan  //在springBoot启动时会自动扫描@WebServlet，并将该类实例化
public class DemoApplication {
 
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

## SpringBoot Tomcat容器

Tomcat打破了双亲委派

## Netty



## Jetty



## Servlet



## Mima



## Nginx



## Tomcat



## SpringBoot CommandRunner和ApplicationRunner

接口是在容器启动成功后的最后一步回调（类似开机自启动）

## CommandLineRunner、ApplicationRunner

开机自启动

## 自定义starter

/Meta-INF/XXX.factories文件注册 @Configuration自动装配

## 事件驱动

在不利用MQ的情况下，业务A处理完后，同时触发B、C、D业务执行。用事件驱动的好处是各个子过程的开发可以专注于自己的业务。

@TransactionalEventListener实现监听事件的事务隔。

Spring事件3个部分组成：ApplicationEvent、ApplicationEventPublisherAware、ApplicationListener

onApplicationEvent方法上加@Async支持异步，在有@EventListener的注解方法上加上@Async。注：启动类上同时要加上@EnableAsync。

## SpringBoot安全

使用HTTPs

## SpringBoot 2.X和1.X版本区别

2.X 响应式编程、至少JDK 1.8、支持Kotlin、支持http 2.0

SpringBoot2单元测试不支持.yml

2.0开始@Deprecated WebMvcConfigurerAdapter，推荐采用WebMvcConfigurer、WebMvcConfigurationSupport

```java
@Configuration
public class WebMvcConfg implements WebMvcConfigurer {
  //省略
}
@Configuration
public class WebMvcConfg extends WebMvcConfigurationSupport {
  //省略
}
```

#