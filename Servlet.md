# Servlet



## 1、主要内容 

![Servlet](C:\Users\EllipticNine\Desktop\MD\LearningForJava\Servlet.png)

## 2、Servlet的实现

是什么？

1、Server and Applet，服务端小程序。使用java编写的服务端程序，可以生产动态Web页。

2、Sevlet本质是java类，但要遵守Servlet编写规范，无main方法，它的创建、使用、销毁都由·容器·进行管理（如：Tomcat）。



## 3、Http协议

### 【请求协议】

#### （1）请求行

​		1、请求方式：Get、Post等

​		2、请求地址

​		3、协议版本

#### （2）请求头

​		1、相关接收信息的键值对

#### （3）请求正文（体）

【注】：Get方法没有请求体，直接写在请求行后面

### 【响应协议】

#### （1）响应行

​		1、http版本、状态码、状态码说明

#### （2）响应头

​		键值对

#### （3）响应正文

​		返回内容

### 【消息头】

##### 请求头

​	允许客户端向服务端传递请求的附加信息及客户端自身的信息。

· Referer：指明请求从哪里来。通过地址栏输入地址访问的都没有该请求头。

##### 响应头

· Location：重定向到新的位置。

· Refresh：自动刷新。





## 4、Tomcat

#### 4.1. 是什么？

稳定的、免费的、开源的、受欢迎的、符合javaee web标准的最小web容器。

#### 4.2. 目录

1、bin ----相关启动脚本

2、conf ---- 配置文件

3、lib ---- 库文件

4、logs ---- 日志

5、temp ---- 临时文件

6、webapps ---- 项目文件（html、图片等）

7、work ---- 存放jsp生产的源码



## 5、编写Servlet类

1、创建普通java类

2、继承 javax.servlet.http.HttpServlet类

3、重写service方法，用来处理请求

4、设置注解，指定访问路径



![image-20210820160312865](C:\Users\EllipticNine\Desktop\MD\LearningForJava\image-20210820160312865.png)

这是项目路径，与项目名不同。



## 6、Servlet工作流程

1、通过请求头获知浏览器访问的是哪个主机

2、通过请求行获知访问的是哪一个web应用

3、通过请求行中的请求路径获知访问的是哪个资源

4、通过获取的资源路径在配置中匹配到真实路径

5、服务器创建servlet对象（若是第一次访问，创建servlet实例并调用init方法进行初始化）

6、调用service（request，response）方法来处理请求和响应的操作

7、调用service完毕后返回服务器，由服务器将response缓冲区的

数据取出，以http响应的格式发送给浏览器



## 7、生命周期

### 一、实例和初始化时机

请求到达容器时，查找该servlet对象是否存在，如果不存在，则会实例化并初始化。

### 二、就绪/调用/服务阶段

1、只要有请求到达容器，容器就会调用servlet对象的`service()`方法

2、处理请求的方法在整个生命周期中可以被多次调用；

3、HttpServlet的service()方法，会依据请求方式来调用`doGet()`和`doPost`方法。但是这两个方法在默认情况下会抛出异常，所以经常会重写。

### 三、销毁时机

当容器关闭时（应用程序会停止），会将程序中的Servlet实例进行销毁。



### 四、请求--响应

【过程】

1、web client 向Servlet容器（Tomcat）发出http请求

2、Servlet容器接收web client 的请求

3、Servlet容器创建一个HttpServletRequest对象，将web client请求的信息封装到这个对象中

4、Servlet容器创建一个HttpServletResponse对象

5、Servlet容器调用HttpServlet对象的service方法，把Response与Request作为参数，传给HttpServlet

6、HttpServlet调用HttpServletRequest对象的有关方法，获取Http请求信息

7、HttpServlet调用HttpServletResponse对象的有关方法，生成响应数据

8、Servlet容器把HttpServlet的响应结果传给web client



## HttpServletRequest对象

【用途】

​	用于接收客户端发送过来的请求信息（如：请求的参数、发送的头信息等）

​	service()方法中形参接收的是HttpServletRequest接口的实例化对象，表示该对象主要应用在Http协议上；该对象由Tomcat封装好后传递过来。

​	ServletRequest的目前唯一一个子接口就是HttpServletRequest





【接收请求常用方法】

```java
getRequestURL(); //获取从http开始，到？前面结束
getRequestURI(); //获取从站点名开始，到？前面结束
getQueryString(); //获取请求中的参数部分
getMethod(); //获取请求方式
getProtocol(); //获取http版本
getContextPath(); //获取webapp名称
```



【获取请求参数】

```java
getParameter(“name”); //获取指定名称的参数
getParameter(String name); //获取指定名称参数的所有值
```



#### 请求乱码问题

原因:

​	Tomcat8版本以前，编码格式为IOS8859-1，Get和Post请求都会乱码。

​	8版本以后都是UTF-8，Get请求不会乱码，Post请求会乱码

解决方法：

​	方式一：设置请求的编码格式

​	`request.setCharacterEncoding("UTF-8");`

​	方式二：通过new String()

​	`new String(request.getParameter(name).getBytes("ISO-8859-1"), "UTF-8");`



#### 请求转发

`request.getRequestDispatch("index.jsp").forward(req, resp);`

1、地址栏不发生改变

2、服务端行为

3、请求转发只有一次请求

4、request对象可以共享



#### request作用域

1、之前的getParameter方法获取的是从页面传递进来的参数，若我们想从后台直接传数据到页面，如何处理？

【答】使用request作用域，`setAttribute()`方法。

//设置作用域

`request.setAttribute(String name, Object value);`

//获取作用域

`request.getAttribute(String name);`

//移除作用域

`request.removeAttribute(String name);`

2、只在一次请求中传递，即：只在请求转发中有效



## HttpServletResponse对象

### 响应数据

有两种形式：

1、getWriter() 字符输出流，向客户端输出字符

2、getOutputStream() 可以向客户端输出任意内容

两种方法不能同时使用，因为一次请求中只有一个流可以使用

```java
//字符流
PrintWriter writer = resp.getWriter();
writer.write("Hello");       
writer.close();
//字节流
ServletOutputStream out = resp.getOutputStream();   out.write("Hello2".getBytes());
out.close();
```



### 响应乱码

【出现原因】

服务端与客户端的编码不一致，导致乱码

【情形】

1、getWriter()字符输出流

​	响应中文必出现乱码，服务端编码默认使用ISO-8859-1编码格式，不支持中文。

2、getOutputStream()字节输出流

​	可能出现乱码，可能正常。

【解决方案】

1、设置客户端与服务端的编码格式一致

2、设置客户端与服务端的编码格式都支持中文



```java
//设置客户端编码
response.setHeader("content-type", "text/html;charset=UTF-8");
//设置服务端编码
response.setCharacterEncoding("UTF-8");
//或同时设置
response.setContentType("text/html;charset=UTF-8");
```



### 重定向

【是什么？】

服务端指导，客户端行为的跳转方式

【特点】

1、地址栏会发生改变

2、客户端跳转

3、有两次请求

4、request作用域不共享



### 请求转发

