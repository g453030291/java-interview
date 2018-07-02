#### 21.restful注解？

#### 22.自定义注解？

用@interface声明一个自定义注解；JDK中自带三个原生（Override(重写)、Deprecated(方法过期)、SuppressWarnings(压制警告)）；JDK中提供四个元注解：（Documented(表明此注解的类可以被JavaDoc文档化)、Inherited(指明该注解类型被自动继承)、Retention(指明在什么级别显示此注解)、Target(该注解的适用范围)）

Retention参数：

RetentionPolicy.SOURCE 注解存在于源代码中，编译时会被抛弃

RetentionPolicy.CLASS 注解会被编译到class文件中，但是JVM会忽略

RetentionPolicy.RUNTIME JVM会读取注解，同时会保存到class文件中

Target参数：

ElementType.TYPE 用于类，接口，枚举但不能是注解

ElementType.FIELD 作用于字段，包含枚举值

ElementType.METHOD 作用于方法，不包含构造方法

ElementType.PARAMETER 作用于方法的参数

ElementType.CONSTRUCTOR 作用于构造方法

ElementType.LOCAL_VERIABLE 作用于本地变量或者catch语句

ElementType.ANNOTATION_TYPE 作用于注解

ElementType.PACKAGE 作用于包

#### 23.二叉树、红黑树的特点？

#### 24.JDK1.7和JDK1.8的区别？

①：Lambda表达式；

②：interface的方法，加上default，就有了默认的实现方法，有方法体；

③：内置了 Base64 编码的编码器和解码器；

④：新增Stream API

#### 25.lambda表达式性能问题？

#### 26.mysql中的左、右、内、外连接？

内连接（inner join）：相等连接-自然连接-交叉连接（CROSSJOIN）

外连接：左外连接-右外连接-全连接

#### 27.接口和抽象类的区别？ 

抽象程度：抽象类->接口->普通类

①：抽象类和接口都不能被直接实例化，如果二者要实例化，就涉及到多态。

②：接口里面只能对方法进行声明，抽象类既可以对方法进行声明也可以对方法进行实现。

③：抽象类里面可以没有抽象方法。

④：如果一个类里面有抽象方法，那么这个类一定是抽象类。

⑤：抽象类主要是用来抽象类别，接口主要是用来抽象方法功能。当你关注事物的本质的时候，请用抽象类；当你关注一种操作的时候，用接口。

#### 28.Java的强、软、弱、虚引用？ 

引用强度排列四种Java引用类型：强引用->软引用->弱引用->虚引用；

强引用：用new来创建一个新对象的引用就是强引用，强引用在程序内存不足（OOM）的时候也不会被回收

软引用：相当于缓存，在内存不够时，会回收软引用的对象。创建缓存的时候，创建的对象放进缓存中，当内存不足时，JVM就会回收早先创建的对象。

弱引用：弱引用就是只要JVM垃圾回收器发现了它，就会将之回收，使用方式

虚引用：虚引用存在的唯一作用就是当它指向的对象被回收后，虚引用本身会被加入到引用队列中（ReferenceQueue），用作记录它指向的对象已被回收。

#### 29.Spring常用注解？ 

@PathVariable：取出URI中的参数

@requestParam：获取参数，类似于request.getparamter();

@Component：将一个bean交给spring管理