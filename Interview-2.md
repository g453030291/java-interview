#### 11.什么情况下会发生死锁，怎么避免死锁？ 

产生死锁四个条件：

互斥条件：一段时间内某资源只由一个进程占用

请求和保持条件：请求进程已经占用了某资源，此时，继续请求其他资源，但资源被其他进程占用，此时，进程被阻塞。

不剥夺条件：资源不能被外部进程剥夺，只能由自己释放

环路等待条件：多个资源相互等待

避免死锁的三种方案：

1.注意加锁顺序（避免环路等待）

2.加锁时限，加上请求锁的timeout时间

3.死锁检测

#### 12.http和https的区别？

#### 13.hashcode和equals？

#### 14.常用的Linux命令（赋予某个用户权限）？

找到/etc/sudoers文件修改其中用户对应的权限。 

#### 15.http协议，请求头，响应头等。 

请求头： Accept（文档格式）: text/html,application/xhtml+xml,application/xml;

Accept-Encoding（压缩格式）: gzip, deflate

Accept-Language（语言）: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;

Connection（连接方式）: keep-alive

Cookie:

 Host（主机地址）: list.tmall.com Referer: https://list.tmall.com/search_product.htm

Upgrade-Insecure-Requests（客户端类型）: 1 User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:59.0) Gecko/20100101 Firefox/59.0

响应头：

（状态码）HTTP/2.0 200 OK

content-encoding（压缩格式）: gzip

content-language（语言、编码格式）: zh-CN content-type: text/html;charset=GBK

date（日期）: Thu, 24 May 2018 13:24:13 GMT

server: Tengine/Aserver

strict-transport-security: max-age=0

timing-allow-origin: *

ufe-result: A6

vary: Accept-Encoding

X-Firefox-Spdy: h2

#### 16.常用算法？ 

#### 17.常用设计模式？ 

#### 18.Nginx的特点？ 

一个master进程管理，多个worker进程工作；

动静态资源，分开请求，加快相应速度；

使用异步非阻塞的事件处理机制；

正向代理；反向代理；负载均衡；邮件服务器；

#### 19.TCP三次握手？ 

#### 20.springboot特有注解？ 