# HTTP协议与TCP协议的区别

1. HTTP对应于应用层

2. TCP对应于传输层

3. HTTP协议建立在TCP协议之上，HTTP在发起请求时通过TCP协议建立起 连接服务器的通道，请求结束则立即断开TCP连接。

   从HTTP/1.1起，默认开启keep-alive属性，保持连接特性，简单地说，**当一个网页打开完成后，客户端与服务器之间用于传输HTTP数据的TCP连接不会关闭，若客户端再次访问该服务器上的网页，会继续使用这一条已经建立的连接，它有一个保持时间，可以设定。

4. HTTP是无状态的短连接，而TCP是有状态的长连接。

   socket：

   ​	socket本身不是协议，而是一个接口调用（API）。socket是对TCP/IP协议的抽象。socket是计算机之间进行**通信**的**一种约定**或一种方式。通过 socket 这种约定，一台计算机可以接收其他计算机的数据，也可以向其他计算机发送数据。



## HTTP content-type

Content-Type，内容类型，一般是指网页中存在的content-type，**用于定义网络文件的类型和网页的编码，决定浏览器将以什么形式、什么编码读取这个文件**。（这就是为什么，一些asp网页点击结果为下载文件或图片）

# HTTP请求格式

请求行 ：请求头 ：空行 ：请求数据

## 常用的请求头

1. Accept
   * Accept: text/html 浏览器可以接受服务器返回的类型为 text/html
   * Accept:\*/\*  代表浏览器可以处理所有类型，一般浏览器发给服务器都是这个
2. Accept-Encoding
   * : gzip, deflate  浏览器申明自己接受的编码方法，通常指压缩方法，是否支持压缩，支持什么压缩方法（gzip，deflate）
3. Accept-Language
   * ：zh-CN   声明接受语言为中文
4. Connection
   * ：keep-alive  打开一个连接之后，客户端与服务端之间用于传输HTTP数据的TCP连接不会关闭，若再次访问，则直接使用这一条已经建立的连接。
   * ：close  代表一个request完成后，TCP通道会关闭，当再次访问时，需要重新建立TCP连接。
5. Host（发送请求时，该报头必须）
   * Host：www.baidu.com  请求报头域主要用于指定被请求资源的Internet主机号和端口号，通常是从URL中提取出来。
6. Referer
   * ：url    当浏览器向web服务器放请求的时候，带上referer可告诉服务器请求来自哪个页面链接（此处为URL）
7. 等等

# HTTP响应格式

状态行 ：消息报头 ：空行 ：响应正文

以上四个部分。

![img](https://www.runoob.com/wp-content/uploads/2013/11/httpmessage.jpg)



# 请求方法

http1.0：

* GET
* POST
* HEAD

http1.1：

* PUT
* PATCH
* DELETE
* OPTIONS
* TRACE
* CONNECT

# 状态码

1xx：指示信息---表示请求已接收，继续处理

2xx：成功---表示请求已被成功接收、理解、接受

3xx：重定向

4xx：客户端错误---语法错误或请求无法实现

5xx：服务端错误---服务器未能实现合法的请求

## 常用状态码：

* 100：该状态码告诉客户端应该继续发送请求，这个临时响应是用来通知客户端的，部分的请求服务器已经接受，但是客户端应继续发送求请求的剩余部分，如果请求已经完成，就忽略这个响应，而且服务器会在请求完成后向客户发送一个最终的结果。
* 200：最为常见的状态码，表示服务器已经成功接受请求，并返回客户端所请求的最终结果。
* 202：表示服务器接受了请求，但还未处理，且会不会处理不确定。
* 204：成功处理了请求，但没有返回任何实体内容，可能返回新的头部元信息。
* 301：客户端请求的网页已经永久移动到新的位置，当链接发生变化时，返回301代码告诉客户端链接的变化，客户端保存新的链接，并向新的链接发出请求，已返回请求结果。
* 404：请求失败，客户端请求的资源没有找到或是不存在。
* 500：服务器遇到未知错误，导致无法完成客户端当前的请求。
* 503：服务器过载或者维护，无法解决当前请求。

一般除了错误的状态码，都不会看到服务器的状态码。