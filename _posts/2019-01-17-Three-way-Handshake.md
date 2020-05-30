---
title: 简述TCP的三次握手过程
key: 20190117
tags: TCP
---

<!--more-->

> TCP 握手协议

> 在 TCP/IP 协议中,TCP 协议提供可靠的连接服务,采用三次握手建立一个连接.

- 第一次握手：建立连接时,客户端发送 syn 包(syn=j)到服务器,并进入 SYN_SEND 状态,等待服务器确认；
  SYN：同步序列编号(Synchronize Sequence Numbers)

- 第二次握手：服务器收到 syn 包,必须确认客户的 SYN（ack=j+1）,同时自己也发送一个 SYN 包（syn=k）,即 SYN+ACK 包,此时服务器进入 SYN_RECV 状态；

- 第三次握手：客户端收到服务器的 SYN ＋ ACK 包,向服务器发送确认包 ACK(ack=k+1),此包发送完毕,客户端和服务器进入 ESTABLISHED 状态,完成三次握手.

> A 与 B 建立 TCP 连接时：首先 A 向 B 发 SYN（同步请求），然后 B 回复 SYN+ACK（同步请求应答），最后 A 回复 ACK 确认，这样 TCP 的一次连接（三次握手）的过程就建立了！

### 一、TCP 报文格式

- TCP/IP 协议的详细信息参看《TCP/IP 协议详解》三卷本。下面是 TCP 报文格式图：

  ![](https://wx1.sinaimg.cn/large/a5caea9fgy1g1ni6jlmcoj20an04odfr.jpg)

- 上图中有几个字段需要重点介绍下：

  - （1）序号：Seq 序号，占 32 位，用来标识从 TCP 源端向目的端发送的字节流，发起方发送数据时对此进行标记。

  - （2）确认序号：Ack 序号，占 32 位，只有 ACK 标志位为 1 时，确认序号字段才有效，Ack=Seq+1。

  - （3）标志位：共 6 个，即 URG、ACK、PSH、RST、SYN、FIN 等，具体含义如下：

  - （A）URG：紧急指针（urgent pointer）有效。

  - （B）ACK：确认序号有效。

  - （C）PSH：接收方应该尽快将这个报文交给应用层。

  - （D）RST：重置连接。

  - （E）SYN：发起一个新连接。

  - （F）FIN：释放一个连接。

- 需要注意的是：

  （A）不要将确认序号 Ack 与标志位中的 ACK 搞混了。

  （B）确认方 Ack=发起方 Seq+1，两端配对。

### 二、三次握手

- 所谓三次握手（Three-Way Handshake）即建立 TCP 连接，就是指建立一个 TCP 连接时，需要客户端和服务端总共发送 3 个包以确认连接的建立。在 socket 编程中，这一过程由客户端执行 connect 来触发，整个流程如下图所示：

  ![](https://wx1.sinaimg.cn/large/a5caea9fgy1g1ni7tk1rij20ed08gwei.jpg)

  （1）第一次握手：Client 将标志位 SYN 置为 1，随机产生一个值 seq=J，并将该数据包发送给 Server，Client 进入 SYN_SENT 状态，等待 Server 确认。

  （2）第二次握手：Server 收到数据包后由标志位 SYN=1 知道 Client 请求建立连接，Server 将标志位 SYN 和 ACK 都置为 1，ack=J+1，随机产生一个值 seq=K，并将该数据包发送给 Client 以确认连接请求，Server 进入 SYN_RCVD 状态。

  （3）第三次握手：Client 收到确认后，检查 ack 是否为 J+1，ACK 是否为 1，如果正确则将标志位 ACK 置为 1，ack=K+1，并将该数据包发送给 Server，Server 检查 ack 是否为 K+1，ACK 是否为 1，如果正确则连接建立成功，Client 和 Server 进入 ESTABLISHED 状态，完成三次握手，随后 Client 与 Server 之间可以开始传输数据了。

- SYN 攻击：

  在三次握手过程中，Server 发送 SYN-ACK 之后，收到 Client 的 ACK 之前的 TCP 连接称为半连接（half-open connect），此时 Server 处于 SYN_RCVD 状态，当收到 ACK 后，Server 转入 ESTABLISHED 状态。SYN 攻击就是 Client 在短时间内伪造大量不存在的 IP 地址，并向 Server 不断地发送 SYN 包，Server 回复确认包，并等待 Client 的确认，由于源地址是不存在的，因此，Server 需要不断重发直至超时，这些伪造的 SYN 包将产时间占用未连接队列，导致正常的 SYN 请求因为队列满而被丢弃，从而引起网络堵塞甚至系统瘫痪。SYN 攻击时一种典型的 DDOS 攻击，检测 SYN 攻击的方式非常简单，即当 Server 上有大量半连接状态且源 IP 地址是随机的，则可以断定遭到 SYN 攻击了，使用如下命令可以让之现行：`netstat -nap | grep SYN_RECV`

### 三、四次挥手

- 三次握手耳熟能详，四次挥手估计就没那么熟悉，所谓四次挥手（Four-Way Wavehand）即终止 TCP 连接，就是指断开一个 TCP 连接时，需要客户端和服务端总共发送 4 个包以确认连接的断开。在 socket 编程中，这一过程由客户端或服务端任一方执行 close 来触发，整个流程如下图所示：

  ![](https://wx1.sinaimg.cn/large/a5caea9fgy1g1ni8u67rcj20e308zjrf.jpg)

- 由于 TCP 连接时全双工的，因此，每个方向都必须要单独进行关闭，这一原则是当一方完成数据发送任务后，发送一个 FIN 来终止这一方向的连接，收到一个 FIN 只是意味着这一方向上没有数据流动了，即不会再收到数据了，但是在这个 TCP 连接上仍然能够发送数据，直到这一方向也发送了 FIN。首先进行关闭的一方将执行主动关闭，而另一方则执行被动关闭，上图描述的即是如此。

  （1）第一次挥手：Client 发送一个 FIN，用来关闭 Client 到 Server 的数据传送，Client 进入 FIN_WAIT_1 状态。

  （2）第二次挥手：Server 收到 FIN 后，发送一个 ACK 给 Client，确认序号为收到序号+1（与 SYN 相同，一个 FIN 占用一个序号），Server 进入 CLOSE_WAIT 状态。

  （3）第三次挥手：Server 发送一个 FIN，用来关闭 Server 到 Client 的数据传送，Server 进入 LAST_ACK 状态。

  （4）第四次挥手：Client 收到 FIN 后，Client 进入 TIME_WAIT 状态，接着发送一个 ACK 给 Server，确认序号为收到序号+1，Server 进入 CLOSED 状态，完成四次挥手。

- 上面是一方主动关闭，另一方被动关闭的情况，实际中还会出现同时发起主动关闭的情况，具体流程如下图：

  ![](https://wx1.sinaimg.cn/large/a5caea9fgy1g1ni97na0uj20dz05b0sp.jpg)

  流程和状态在上图中已经很明了了，在此不再赘述，可以参考前面的四次挥手解析步骤。

### 四、更多

- 关于三次握手与四次挥手通常都会有典型的面试题，在此提出供有需求的圆媛猿们参考：

  （1）三次握手是什么或者流程？四次握手呢？

  答案前面分析就是。

  （2）为什么建立连接是三次握手，而关闭连接却是四次挥手呢？

  这是因为服务端在 LISTEN 状态下，收到建立连接请求的 SYN 报文后，把 ACK 和 SYN 放在一个报文里发送给客户端。而关闭连接时，当收到对方的 FIN 报文时，仅仅表示对方不再发送数据了但是还能接收数据，己方也未必全部数据都发送给对方了，所以己方可以立即 close，也可以发送一些数据给对方后，再发送 FIN 报文给对方来表示同意现在关闭连接，因此，己方 ACK 和 FIN 一般都会分开发送。
