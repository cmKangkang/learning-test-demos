# HTTP

HTTP是Hyper Text Transfer Protocol（超文本传输协议）的缩写。

**HTTP协议用于WWW服务器传输超文本到本地浏览器的传输协议**。它可以使浏览器更加高效，使网络传输减少。保证计算机能正确快速的传输超文本文档，还确定传输文档中的哪一部分，以及哪部分内容首先显示。

## 在TCP/IP协议栈中的位置

通常承载与TCP协议之上，有时也承载与TLS或SSL协议层之上。![img](http://files.jb51.net/upload/201108/20110826201312465.jpg)

默认HTTP的端口号为80，HTTPS的端口号为443.



## HTTP请求响应模型

永远都是客户端发起请求，服务器回送响应。

![img](http://files.jb51.net/upload/201108/20110826201312757.jpg)

如此就限制了使用HTTP协议，无法实现在客户端没有发起请求的时候，服务端将消息推送给客户端。

HTTP协议是一个无状态的协议，同一个客户端的这次请求和上次请求没有对应关系。



## 工作流程

一次HTTP操作称为一个事务，其工作过程分为四步：

1. 首先，客户机与服务器需要建立。只要单击超链接或者发送Ajax请求，HTTP的工作开始。
2. 建立连接后，客户机发送一个请求给服务器，请求方式格式为：URL、协议版本号、MIME信息（包含请求修饰符、客户机信息和可能内容）
3. 服务器收到请求后，给与相应的响应信息，其格式为：一个状态行，包括信息的协议版本号、一个成功或错误的代码，后边是MIME信息包括服务器信息、实体信息和可能的内容。
4. 客户端接收服务器返回的信息，然后客户机与服务器断开连接。

`总结`：建立连接-->客户机发送请求给服务器-->服务器收到请求，返回响应信息-->客户端接收信息，然后断开连接



## 头域

每个头域由一个域名，冒号（:）和域值三部分组成。域名是大小写无关的，域值前可以添加任何数量的空格符，头域可以被扩展为多行，在每行开始处，使用至少一个空格或制表符。

### host头域

指定请求资源的Internet主机和端口号，必须标识请求URL的原始服务器或网关的位置。

HTTP/1.1请求必须包含主机头域，否则系统会以400状态码返回。

### Reference头域

Referer头域允许客户端指定请求uri的源资源地址，这可以允许服务器生成回退链表，可用来登陆、优化cache等。他也允许废除的或错误的连接由于维护的目的被追踪。如果请求的uri没有自己的uri地址，Referer不能被发送。如果指定的是部分uri地址，则此地址应该是一个相对地址。

### User-Agent

User-Agent头域的内容包含发出请求的用户信息。

### cache-control

Cache-Control指定请求和响应遵循的缓存机制。在请求消息或响应消息中设置Cache-Control并不会修改另一个消息处理过程中的缓存处理过程。

### Date头域

Date头域表示消息发送的时间，时间的描述格式由rfc822定义。



## HTTP  的几个重要概念

### 连接：Connection

一个传输层的实际环流，它是建立在两个相互通讯的应用程序之间。

在http1.1，request和reponse头中都有可能出现一个connection的头，此header的含义是当client和server通信时对于长链接如何进行处理。

在http1.1中，client和server都是默认对方支持长链接的， 如果client使用http1.1协议，但又不希望使用长链接，则需要在header中指明connection的值为close；如果server方也不想支持长链接，则在response中也需要明确说明connection的值为close。不论request还是response的header中包含了值为close的connection，都表明当前正在使用的tcp链接在当天请求处理完毕后会被断掉。以后client再进行新的请求时就必须创建新的tcp链接了。



### 消息：Message

HTTP通讯的基本单位，包含一个结构化的八元组序列并通过连接传输。

### 请求：Request

一个从客户端到服务器的请求信息包括应用于资源的方法、资源的标识符和协议的版本号。

### 响应：Response

一个从服务器返回的信息包括HTTP协议的版本号、请求的状态（例如“成功”或“没找到”）和文档的MIME类型。

### 资源：Resource

由URI标识的网络数据对象或服务

### 实体：Entity

数据资源或来自服务资源的回应的一种特殊表示方法，它可能被包含在一个请求或响应信息中。一个实体包括实体头信息和实体本身内容。

### 客户机：Client

一个为发送 请求 而建立连接的应用程序

### 用户代理：User'Agent

初始化一个请求的客户机。他们是浏览器、编辑器或其他用户工具。

### 服务器：Server

一个接受连接并对 请求 返回信息的应用程序

### 源服务器：Origin server

是一个给定资源可以在其上驻留或被创建的服务器。

### 代理：proxy

一个中间程序，它可以充当一个服务器，也可以充当一个客户机，为其它客户机建立请求。

请求是通过可能的翻译在内部或经过传递到其它的服务器中。一个代理在发送请求信息之前，必须解释并且如果可能重写它。

代理经常作为通过防火墙的客户机端的门户，代理还可以作为一个帮助应用来通过协议处理没有被用户代理完成的请求。



### 网关：Gateway

一个作为其它服务器中间媒介的服务器。与代理不同的是，网关接受请求就好象对被请求的资源来说它就是源服务器；发出请求的客户机并没有意识到它在同网关打交道。

网关经常作为通过防火墙的服务器端的门户，网关还可以作为一个协议翻译器以便存取那些存储在非HTTP系统中的资源。

### 通道：Tunnel

是作为两个连接中继的中介程序。

一旦激活，通道便被认为不属于HTTP通讯，尽管通道可能是被一个HTTP请求初始化的。当被中继的连接两端关闭时，通道便消失。当一个门户(Portal)必须存在或中介(Intermediary)不能解释中继的通讯时通道被经常使用。

### 缓存：Cache

反应信息的局域存储。