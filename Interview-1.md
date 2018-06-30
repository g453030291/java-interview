#### 1.Java线程有几种状态，分别是什么？ 

线程的状态定义在java.lang.Thread.State下有一个eum类，其中定义了线程的6种状态：

new：线程尚未启动

runnable：线程运行中

blocked：多个线程有同步操作的场景，如正在等待synchronize释放等

waiting：线程拥有了某个锁之后，调用了他的wait方法，等待其他线程调用notify

（blocked和wating都是等待，不同的是，blocked是在临界点之外等待，而wating是在临界点内wait等待notify唤醒）

timed_waiting：有时间限制的waiting，调用了wait(long)，join(long)等

terminated：执行结束的线程

#### 2.介绍一下MySQL的四种事务隔离级别？

（这个我绝对看过NNNN多遍.....感觉大佬不会问这种问题吧...就没有认真记...结果悲剧了） 

read uncommitted（**读未提交**）：会产生**脏读、幻读、不可重复读**的问题，既，会读取到还未commit的数据

read committed（读其他事务提交的数据）：当前会话可以读取到其他事务提交后的数据，避免脏读，但会产生产生**不可重复读、幻读**的后果

repeatable read（**可重复读**）-MySql默认隔离级别：在同一个事务中，查询出的结果总是一致的（解决了脏读、不可重复读的问题），会产生**幻读**的问题（在其他会话中插入的数据，当前会话查询不出结果，但是进行数据操作时，可能报错）

serializable（串行化）：一个事务对数据进行操作时，另一个事物在进入操作该数据，事物会被挂起（有超时时间），等待前一个事务的完成，在进行当前事务的操作（性能较差）（也就是数据库不存在并发访问的情况，都去排队依次执行）

（脏读：读到其他事物未提交的数据，如果这些数据回滚，这次读到的数据就是无效的；不可重复读：一个事务中，读到其他事务提交后的数据，导致查询结果不一致；幻读：同一事物中，查询结果一致，但其他事物提交了数据，当前事务没有读取到，当前事务再进行数据操作，会产生主键冲突等报错。）

#### 3.Spring的事务？ 

事务四大特性：ACID，原子性、一致性、隔离性、持久性

Spring中为事务管理提供了三个接口：

PlatformTransactionManager：事务管理器（Spring定义了一个顶级的事务管理接口类，具体实现由各ORM框架负责，比如常用的DataSourceTransactionManager）

TransactionDefinition：事务定义信息（隔离级别、传播行为、只读、超时）

TransactionStatus：事务运行状态

![](G:\笔记\images\事务传播行为(七种).png)

#### 4.AtomicInteger和加了volatile的Integer有什么区别？ 

这道题核心还是在考察多线程环境当中变量的安全性。众所周知，AtomicInteger利用CAS原理，保证了多线程环境当中变量的安全。但是，用volatile修饰的Integer却不一定是线程安全的。虽然volatile保证了各个线程在取出volatile修饰的变量时都能拿到最新的值，但是，当各个线程去向volatile变量进行写操作的时候（比如++），会存在一种情况，比如volatile Integer i=1；此时，A、B两个线程同时取到i，都进行++的操作，此时由于CPU时间分片的问题，可能A首先写入，i变成了2，B再向i写入的时候，期望i=1->2。但实际情况，并不是这样。所以volatile并不能保证绝对的线程安全。 

#### 5.kafka的权重优先级配置？

#### 6.hashmap的contains方法？

根据key的hash值和key获取对应的节点；

调用getNode方法，首先检测hash表是否为空或key对应的桶是否为空，不为空，就去判断下面的节点，是什么样的数据结构，如果是红黑树就遍历树取出节点，如果为链表就遍历链表。

#### 7.过滤器、监听器、拦截器各自的作用？ 

过滤器（Filter）：

作用：过滤所有web请求，基于servlet。

应用：设置统一编码、过滤掉非法字符等。

实现：实现Filter接口，接口中有三个方法init（filterConfig）、doFilter（request，response，filterChain）、destroy。web容器启动时，会调用init方法初始化一个filter对象实例，请求进入后，调用doFilter在调用方法前后执行操作，结束后，调用filterChain对象，执行下一个过滤器。filterConfig可以获取到拦截器的各种属性（filter名、各种参数等）。

监听器（Listener）：

作用：做一些初始化的操作，设置一些基本参数或者固定对象等。基于servlet。

应用：统计当前在线人数。

实现：实现ServletContextListener接口，接口中有两个方法，contextInitialized(ServletContextEvent)；contextDestroyed(ServletContextEvent);一个初始化，一个销毁。

拦截器（Interceptor）：

作用：类似于AOP，在某个controller方法前后执行。基于反射机制，JDK的动态代理实现的。它依赖于具体的接口，使用时动态的生成字节码。

应用：可以用于角色、权限认证。

实现：Spring的拦截器，实现HandlerInterceptorAdapter接口，preHandle（request，reponse，objectHandle）、postHandle（request，reponse，objectHandle，modelAndView）、afterCompletion（request，reponse，objectHandle，exception）。preHandle在执行方法前调用，postHandle在执行方法后调用，afterCompletion在dispatcherServlet完全处理完请求后被调用，常用于销毁资源。

#### 8.跨域常用解决方案？

#### 9.说一下java中的GC？

![](G:\笔记\images\java内存区域模型.png)

JVM总体分为堆和非堆两个区域。堆是给开发者使用的，非堆部分主要是给JVM自己使用的。

（1）.方法区（包括运行时常量池）：用于保存JVM加载类的信息、常量、静态变量，是各个线程共享的内存区域。

运行时常量池：

（2）.虚拟机栈：每个方法执行的时候，会创建一个“栈帧”。用于存储局部变量表、操作栈、方法出口信息。每个方法从被调用到执行完的过程，就对应着一个栈帧在虚拟机栈中从入栈到出栈的过程。（局部变量表中保存着8种基本数据类型和对象的引用（指针，并非对象本身））。

（3）.本地方法栈：运行Native方法。

（4）.堆：JVM所管理的最大的一块内存区域，也是被各个线程共享的内存区域，在JVM启动时创建。该区域存放了对象的实例、数组（所有new的对象）。-Xms（最小值）-Xmx（最大值），通常将两个值调整为一样大小（避免运行时频繁调整Heap大小）。

堆分为新生代和老年代，新生代又由Eden Space和两块相同大小的Survivor Space组成。程序新创建的对象都从新生代分配内存，老年代用于存放进行多次GC仍然存活的对象。新建的对象也可能直接进入老年代①：可以通过启动参数设置-XX:PretenureSizeThreshold=1024，超过多大就直接在老年代分配，②：大的数组对象。

（5）.程序计数器：最小的一块内存区域，作用是当前线程执行字节码的信号指示器，在程序执行过程中，就是通过计数器实现分支、循环、异常处理、线程恢复等工作。

为了便于垃圾回收，堆分为三个区域，新生代，老年代，持久代。

#### 10.索引失效的原因，及解决方案？ 