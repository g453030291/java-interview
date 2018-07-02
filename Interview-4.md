#### 关键字：

volatile特性：  1. 内存可见性（当一个线程修改volatile变量的值时，另一个线程就可以实时看到此变量的更新值）  2. 禁止指令重排（volatile变量之前的变量执行先于volatile变量执行，volatile之后的变量执行在volatile变量之后）

Transient:

1.用于来表示一个域，不使用serialization来进行序列化。

2.transient关键字，有什么作用？

(1)HashMap中存储的值得大小始终是小于数组大小的，如果使用默认的serialization，	没有元素的位置也会被存储，就会产生不必要的浪费

(2)对于不同的虚拟机，不同的hashCode产生的值，可能会不同。反序列化之后元素的	位置和之前是保持一致的，但是indexOf()返回的元素下标会不同

#### HTTP协议：

状态码：

3XX：浏览器需要执行某些特殊处理，重定向请求

302：临时移动，客户端还应使用原有的URI

4XX：客户端语法错误，服务器无法解析

5XX：服务器内部错误，

http执行过程：

1. 域名解析，查看缓存，或者访问DNS服务器，获取到对应主机的IP地址
2. 发起TCP的三次握手
3. 建立TCP连接后发起http请求
4. 服务器响应http请求，浏览器得到html代码
5. 浏览器解析代码，并请求其中的静态资源

浏览器对页面进行渲染返回给用户

http协议的格式：

分为三部分，起始行、消息头、消息体。之间用CRLF(回车)区分。

头部又分为请求头和响应头，会形成GET /index.html HTTP/1.1格式。响应头一般为HTTP/1.1 200 OK这种格式。

消息头，有很多键值对的说明。比如：connection、content-length、content-type、server等

消息体，GET请求没有消息体，POST请求会将表单数据放在消息体当中，平时调用的API返回的JSON数据都会放在消息体当中

#### RESTful:

特点：面向资源、松耦合、无状态、易扩展

URI 设计：

因为是面向资源，所以用URI指向某个资源，URI中也尽量使用名词。不用比如getXX等动词。

如果有多版本，通常会把版本号放在URI前边，其他的分页、查询等参数，拼接在？之后。

设计URI时尽量使用小写，用中横岗(—)不用下划线(_)。

HTTP Method：

HTTP 协议定义了 8 个 Method，在 Restful API 设计中，我们常用 POST，DELETE，PUT，GET 四方法来操作资源。其中 POST 表示创建资源，DELETE 表示删除某个资源，PUT 表示更新某个资源，GET 表示查询资源。

在设计 Restful API 时，应该遵循 HTTP 关于 “安全性” 和 “幂等性” 的要求。

安全性：无论请求多少次，都不会改变资源的状态。比如 GET 操作，无论执行多少遍，都不会改变资源的状态。所以对于 GET 类 API，在编写应用端代码时，切记要尽可能避免出现删除或者更新数据的逻辑。

幂等性：无论是执行一次，还是执行多次，效果是等价的，比如 DELETE，PUT 操作。以 DELETE 操作为例，删一次和删多次，效果都是该资源不存在了。

![http-restful.png](https://github.com/g453030291/java-interview/blob/master/images/http-restful.png)

Response Code：

请求成功：

200 OK: 请求已成功，Body 有返回内容。多用作 GET Method 的 API 的返回码。

201 Created: 请求已经被实现，资源被创建。多用作 POST Method 的同步类型 API 的返回码。

202 Accepted: 服务器已接受请求，但尚未处理。多用作 POST Method 异步类型 API 的返回码。

204 No Content: 服务器成功处理了请求，没有返回任何内容。用多于 DELETE／PUT Method 的 API 的返回码。

因客户端原因导致请求失败：

400 Bad Request: 如参数错误，格式错误

401 Unauthorized: 用户未被认证，如用密码错误，证书错误

403 Forbidden: 用户权限不够

404 Not Found: 服务端无此资源。通常为 URL 不存在，或者某个 Method 不存在

409 Conflict: 请求存在冲突无法处理该请求

因服务端原因导致请求失败：

500 Internal Server Error: 服务端错误消息，服务器遇到了一个未曾预料的状况。这是最常用的服务端错误代码

501 Not Implemented: 服务器不支持当前请求所需要的某个功能

503 Service Unavailable: 如服务器维护或者过载等

编码：(UTF-8)

在 HTTP 协议中，Accept-Charset／Content-Type 头部可以指定字符编码方案。

Requst 头部: Accept-Charset: utf-8

Response 头部: Content-Type: charset=utf-8

序列化：(XML／SOAP／JSON 等都是序列化和反序列化协议，其中 XML 多用于 html 类型		的应用，而 JSON 成为 html 应用以外的主流序列化和反序列化协议)

在 HTTP 协议中，Accept／Content-Type 头部可以指定序列化和反序列化协议。

Requst 头部: Accept: application/json

Response 头部: Content-Type: application/json

HTTPS:

RESTful推荐使用https协议。(默认端口443)

#### Java线程池(java.util.concurrent.ThreadPoolExecutor

public ThreadPoolExecutor(int corePoolSize,

​                              int maximumPoolSize,

​                              long keepAliveTime,

​                              TimeUnit unit,

​                              BlockingQueue<Runnable> workQueue,

​                              ThreadFactory threadFactory,

​                              RejectedExecutionHandler handler)

ThreadPoolExecutor是线程池的核心类，其中有四个构造方法，其他三个构造方法都是调用上面这个7个参数的构造方法。

##### 参数释义：

1.corePoolSize：核心池的大小，这个参数跟后面讲述的线程池的实现原理有非常大的关系。在创建了线程池后，默认情况下，线程池中并没有任何线程，而是等待有任务到来才创建线程去执行任务，除非调用了prestartAllCoreThreads()或者prestartCoreThread()方法，从这2个方法的名字就可以看出，是预创建线程的意思，即在没有任务到来之前就创建corePoolSize个线程或者一个线程。默认情况下，在创建了线程池后，线程池中的线程数为0，当有任务来之后，就会创建一个线程去执行任务，当线程池中的线程数目达到corePoolSize后，就会把到达的任务放到缓存队列当中；

2.maximumPoolSize：线程池最大线程数，这个参数也是一个非常重要的参数，它表示在线程池中最多能创建多少个线程

3.keepAliveTime：表示线程没有任务执行时最多保持多久时间会终止。默认情况下，只有当线程池中的线程数大于corePoolSize时，keepAliveTime才会起作用，直到线程池中的线程数不大于corePoolSize，即当线程池中的线程数大于corePoolSize时，如果一个线程空闲的时间达到keepAliveTime，则会终止，直到线程池中的线程数不超过corePoolSize。但是如果调用了allowCoreThreadTimeOut(boolean)方法，在线程池中的线程数不大于corePoolSize时，keepAliveTime参数也会起作用，直到线程池中的线程数为0

4.unit：参数keepAliveTime的时间单位，有7种取值，在TimeUnit类中有7种静态属性

(TimeUnit是concurrent包中的一个枚举类：TimeUnit.DAYS; //天TimeUnit.HOURS; //小时TimeUnit.MINUTES;  //分钟TimeUnit.SECONDS;  //秒TimeUnit.MILLISECONDS; //毫秒 TimeUnit.MICROSECONDS;  //微妙TimeUnit.NANOSECONDS; //纳秒)

5.workQueue：一个阻塞队列，用来存储等待执行的任务，这个参数的选择也很重要，会对线程池的运行过程产生重大影响，一般来说，这里的阻塞队列主要有以下几种选择:ArrayBlockingQueue,LinkedBlockingQueue,SynchronousQueue

6.threadFactory：线程工厂，主要用来创建线程

7.handler：表示当拒绝处理任务时的策略，有以下四种取值：

ThreadPoolExecutor.AbortPolicy:丢弃任务并抛出RejectedExecutionException异常。 

ThreadPoolExecutor.DiscardPolicy：也是丢弃任务，但是不抛出异常。 

ThreadPoolExecutor.DiscardOldestPolicy：丢弃队列最前面的任务，然后重新尝试执行任务（重复此过程）

ThreadPoolExecutor.CallerRunsPolicy：由调用线程处理该任务 

##### 重要方法:

excute(),submit(),shutdown(),shutdownNow()

execute()方法实际上是Executor中声明的方法，在ThreadPoolExecutor进行了具体的实现，这个方法是ThreadPoolExecutor的核心方法，通过这个方法可以向线程池提交一个任务，交由线程池去执行。

submit()方法是在ExecutorService中声明的方法，在AbstractExecutorService就已经有了具体的实现，在ThreadPoolExecutor中并没有对其进行重写，这个方法也是用来向线程池提交任务的，但是它和execute()方法不同，它能够返回任务执行的结果，去看submit()方法的实现，会发现它实际上还是调用的execute()方法，只不过它利用了Future来获取任务执行结果（Future相关内容将在下一篇讲述）。

　shutdown()和shutdownNow()是用来关闭线程池的。

##### 任务提交给线程池之后的处理策略:

如果当前线程池中的线程数目小于corePoolSize，则每来一个任务，就会创建一个线程去执行这个任务；

如果当前线程池中的线程数目>=corePoolSize，则每来一个任务，会尝试将其添加到任务缓存队列当中，若添加成功，则该任务会等待空闲线程将其取出去执行；若添加失败（一般来说是任务缓存队列已满），则会尝试创建新的线程去执行这个任务；

如果当前线程池中的线程数目达到maximumPoolSize，则会采取任务拒绝策略进行处理；

如果线程池中的线程数量大于 corePoolSize时，如果某线程空闲时间超过keepAliveTime，线程将被终止，直至线程池中的线程数目不大于corePoolSize；如果允许为核心池中的线程设置存活时间，那么核心池中的线程空闲时间超过keepAliveTime，线程也会被终止。

##### 任务缓存队列及排队策略:

在前面我们多次提到了任务缓存队列，即workQueue，它用来存放等待执行的任务。

workQueue的类型为BlockingQueue<Runnable>，通常可以取下面三种类型：

1）ArrayBlockingQueue：基于数组的先进先出队列，此队列创建时必须指定大小；

2）LinkedBlockingQueue：基于链表的先进先出队列，如果创建时没有指定此队列大小，则默认为Integer.MAX_VALUE；

3）synchronousQueue：这个队列比较特殊，它不会保存提交的任务，而是将直接新建一个线程来执行新来的任务。

##### 任务拒绝策略:

ThreadPoolExecutor.AbortPolicy:丢弃任务并抛出RejectedExecutionException异常。 	ThreadPoolExecutor.DiscardPolicy：也是丢弃任务，但是不抛出异常。 	ThreadPoolExecutor.DiscardOldestPolicy：丢弃队列最前面的任务，然后重新尝试执行任务（重复此过程） 	ThreadPoolExecutor.CallerRunsPolicy：由调用线程处理该任务

##### JDK推荐:

Executors.newCachedThreadPool();        //创建一个缓冲池，缓冲池容量大小为Integer.MAX_VALUE

Executors.newSingleThreadExecutor();   //创建容量为1的缓冲池

Executors.newFixedThreadPool(int);    //创建固定容量大小的缓冲池

#### Java中的异常：

Java中所有异常和错误的超类是Throwable，它有两个字类Error和Exception。

Error是严重到系统不能处理的系统类错误，如：内存溢出、虚拟机错误、栈溢出等。这类错误一般由硬件引起，通常通知系统去处理，程序无法捕获处理。

Exception是用于捕获编写程序时无法预料的情况，如中断异常、非法存取等。为了保证程序的健壮性，java要求必须对这些可能出现的异常进行捕获，并对其进行处理。

RuntimeException是Exception的子类。是那些可能在java虚拟机运行期间抛出异常的超类。

#### Hashmap的contains方法

#### 浏览器跨域请求