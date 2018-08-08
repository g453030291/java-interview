### **关键字：**

#### volatile： 

1. 内存可见性（当一个线程修改volatile变量的值时，另一个线程就可以实时看到此变量的更新值） 
2. 禁止指令重排（volatile变量之前的变量执行先于volatile变量执行，volatile之后的变量执行在volatile变量之后）

#### Transient:

1.用于来表示一个域，不使用serialization来进行序列化。

2.transient关键字，有什么作用？

(1)HashMap中存储的值得大小始终是小于数组大小的，如果使用默认的serialization，	没有元素的位置也会被存储，就会产生不必要的浪费

(2)对于不同的虚拟机，不同的hashCode产生的值，可能会不同。反序列化之后元素的	位置和之前是保持一致的，但是indexOf()返回的元素下标会不同

### **HTTP协议：**

#### 状态码：

3XX：浏览器需要执行某些特殊处理，重定向请求

302：临时移动，客户端还应使用原有的URI

4XX：客户端语法错误，服务器无法解析

5XX：服务器内部错误，

 

#### http执行过程：

1. 域名解析，查看缓存，或者访问DNS服务器，获取到对应主机的IP地址

2. 发起TCP的三次握手

3. 建立TCP连接后发起http请求

4. 服务器响应http请求，浏览器得到html代码

5. 浏览器解析代码，并请求其中的静态资源

浏览器对页面进行渲染返回给用户

#### http协议的格式：

分为三部分，起始行、消息头、消息体。之间用CRLF(回车)区分。

头部又分为请求头和响应头，会形成GET /index.html HTTP/1.1格式。响应头一般为HTTP/1.1 200 OK这种格式。

消息头，有很多键值对的说明。比如：connection、content-length、content-type、server等

消息体，GET请求没有消息体，POST请求会将表单数据放在消息体当中，平时调用的API返回的JSON数据都会放在消息体当中

### **RESTful:**

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

| Method | 安全性 | 幂等性 | 是否有request body | 是否有response body |
| :----: | :----: | :----: | :----------------: | :-----------------: |
|  POST  |   否   |   否   |         是         |         是          |
| DELETE |   否   |   是   |         否         |       最好无        |
|  PUT   |   否   |   是   |         是         |       Option        |
|  GET   |   是   |   是   |         否         |         是          |

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