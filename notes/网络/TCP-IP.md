# TCP/IP

TCP/IP不是一个协议，而是一个协议族。

包含IP协议，IMPC协议，TCP协议，以及HTTP、FTP、POP3协议等。

![img](https://upload-images.jianshu.io/upload_images/2964446-1fd7a0f3216c0530.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/284/format/webp)

TCP为传输层的协议。



**应用层：**

向用户提供一组常用的应用程序：

* 电子邮件
* 文件传输访问
* 远程登陆

**传输层**

提供应用程序间的通信。功能包括：

* 格式化信息流
* 提供可靠传输：为实现该点，传输层协议规定接收端必须发回确认，并且假如分组丢失，必须重新发送。

**网络层**

负责相邻计算机之间的通信。其功能包括三个方面：

* 处理来自传输层的分组发送请求，收到请求后，将分组装入IP数据报，填充报头，选择去往信宿机的路径，然后将数据报发往适当的网络接口。
* 处理输入数据报：首先检查其合法性，然后进行寻径。（假如该数据报已到达信宿机，则去掉报头，将剩下部分交给适当的传输协议；假如该数据报尚未到达信宿，则转发该数据报。）
* 处理路径、流控、拥塞。

**网络接口层**

这是TCP/IP软件的最低层，负责接收IP数据报并通过网络发送，或者从网络上收取物理帧，抽出IP数据报，交给IP层。



`总结`:

* 应用层提供应用层序（电子邮件等）--->TELNET、SMTP、SMTP
* 传输层负责程序（进程）间通信-->TCP
* 网络层负责计算机间通信--->IP
* 网络接口层



## IP是无连接的

IP用于计算机间通信。

IP协议为无连接的通信通信协议。它不会占用两个正在通信的计算机之间的通信线路。如此IP降低了对网络线路的需求。每条线路可以同时满足许多不同计算机之间的通信需要。

IP协议将数据分割为小的独立的包，通过网络在计算机之间传送。IP负责将每个包路由至它的目的地。



## IP地址

每个计算机必须有一个IP地址才能够连入因特网。

每个IP包必须有一个地址才能发送到另一台计算机。

网络上每一个节点都必须要有一个独立的IP地址。

IPv4标准：32位，分为4组，也即255.255.255.255的样式。地址被分为5类，常用的为B类地址。Ip地址为网络号+主机号。



## TCP使用固定连接

TCP用于程序之间的通信。

当应用程序希望通过TCP与另一个应用程序通信时，他会发送一个通信请求。这个请求必须被送到一个确切的地址。在双方握手之后，TCP将在两个应用程序之间建立一个全双工的通信。

这个全双工的通信将占用两个计算机之间的通信线路，直到它被一方或双方关闭为止。

UDP与TCP很相似，但是更简单，同时可靠性低于TCP。



## IP路由器

当一个IP包从一台计算机被发送，它会到达一个IP路由器。

IP路由器负责将这个包 路由 至它的目的地，直接或通过其他的路由器。

在一个相同的通信中，一个包所经由的路径可能会和其他的包不同，而路由器负责根据通信量、网络中的错误或者其他参数来进行正确寻址。



## 域名

用于TCP/IP地址的名字被称为域名。

当键入一个域名，域名就会被DNS程序翻译为数字。（DNS服务器负责将域名翻译为TCP/IP地址，同时负责 使用新的域名信息更新彼此的系统。当一个新的域名连同其 TCP/IP 地址一同注册后，全世界的 DNS 服务器都会对此信息进行更新。



## TCP/IP

TCP/IP 意味着TCP与IP在一起协同工作。

* TCP负责应用程序和网络软件之间的通信。

  IP负责计算机之间的通信。

* TCP负责将数据分割并装入IP包，然后在他们到达的时候重新组合它们。

  IP负责将包发送至接收者。

## TCP报文格式

略

## TCP三次握手

ACK：确认值(Acknowledgement)，为1便是确认连接。

ack：确认编号，即接收上一次远端主机传来的seq然后+1，再发送给远端主机。提示远端主机已经接收上一次所有数据。

三次握手即建立TCP连接，就是指建立一个TCP连接时，需要客户端和服务端总共发送三个包以确认连接的建立。**在socket编程中，这一过程由客户端执行connect来触发。**

1、第一次握手：建立连接时，客户端发送SYN包（SYN=i）到服务器，并进入到SYN-SEND状态，等待服务器确认

2、第二次握手：服务器收到SYN包，必须确认客户的SYN（ack=i+1）,同时自己也发送一个SYN包（SYN=k）,即SYN+ACK包，此时服务器进入SYN-RECV状态

3、第三次握手：客户端收到服务器的SYN+ACK包，向服务器发送确认报ACK（ack=k+1）,此包发送完毕，客户端和服务器进入ESTABLISHED状态，完成三次握手，客户端与服务器开始传送数据。



```text
参考回答：
第一次握手：
起初两端都处于CLOSED关闭状态，Client将标志位SYN置为1，随机产生一个值seq=x，并将该数据包发送给Server，Client进入SYN-SENT状态，等待Server确认；

第二次握手：
Server收到数据包后由标志位SYN=1得知Client请求建立连接，Server将标志位SYN和ACK都置为1，ack=x+1，随机产生一个值seq=y，并将该数据包发送给Client以确认连接请求，Server进入SYN-RCVD状态，此时操作系统为该TCP连接分配TCP缓存和变量；

第三次握手：
Client收到确认后，检查ack是否为x+1，ACK是否为1，如果正确则将标志位ACK置为1，ack=y+1，并且此时操作系统为该TCP连接分配TCP缓存和变量，并将该数据包发送给Server，Server检查ack是否为y+1，ACK是否为1，如果正确则连接建立成功，Client和Server进入ESTABLISHED状态，完成三次握手，随后Client和Server就可以开始传输数据。
```



## TCP四次挥手

四次挥手即终止TCP连接，指断开TCP连接时，需要客户端和服务端总共发送4个包以确认连接的断开。

由于TCP为全双工连接，因此每个方向都需要单独进行关闭。

**在socket编程中，这一过程由客户端或服务端任一方执行close来触发。**



## 为何建立时3次挥手，断开却是4次挥手？

这是因为服务端在LISTEN状态下，收到建立连接请求的SYN报文后，把ACK和SYN放在一个报文里发送给客户端。而关闭连接时，当收到对方的FIN报文时，仅仅表示对方不再发送数据了但是还能接收数据，己方也未必全部数据都发送给对方了，所以己方可以立即close，也可以发送一些数据给对方后，再发送FIN报文给对方来表示同意现在关闭连接，因此，己方ACK和FIN一般都会分开发送。