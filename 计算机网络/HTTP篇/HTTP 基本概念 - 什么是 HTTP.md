# HTTP 基本概念 - 什么是 HTTP

# 开篇

在我们日常享受网络带来的便利与舒适时，或许值得回顾一下：HTTP协议的起源和发展历程。HTTP最初的形态是什么样子的？它是如何不断演进并成为今天几乎主导整个互联网世界的技术呢？

# 什么是 HTTP？

http是超文本传输协议，最初设计用于在实验室或者小型办公环境内分享和传递html页面。在了解它是什么前，我们先看看它是如何诞生，如何发展的。

## 发展历程

随着互联网的普及以及互联网应用的不断发展和突破性进展，http也进行了多次更新与演变，推出了多个版本，以下是http的发展时间线，也简单聊下它的发展历程：

- http/0.9：1991年
    - http/0.9作为最早的版本于1991年问世，并极大地促进了web的发展。该版是一个最小化协议，只能支持客户端通过 get请求方法从服务器上获取静态文档（html 文档）并且不能发送其他任何类型的数据。
- http/1.0：1996年
    - 在http/0.9之后，http/1.0版本于1996年发布，包含了一些重要的特性，例如使用不同的请求方法、具备更好的缓存机制和完善的错误处理等功能。http/1.0还引入了状态码，用于向客户端表明请求结果的状态，例如200 ok表示请求成功，400 bad request表示请求有误等等。
- http/1.1：1999年
    - 虽然http/1.0已经很稳定，但仍存在一些问题，例如，一个tcp连接只能同时发送一个请求，而且一旦建立连接，就需要完成整个请求-响应-关闭流程。为了解决这个问题，http/1.1在持久连接（persistent connections）的基础上，增加了管道(pipelining)技术，允许一个tcp连接同时发送多个请求和响应，这样可以更快地下载页面。同时还引入了缓存管理方案，使用chunked带来更好的流式数据传输，从而提高网络速度。
- http/2.0：2015年
    - 旨在更好地满足现代web的需求，包括提高性能。http/2.0 也更新了一些重要特性：
        - **多路复用**：http/2.0支持同时发送多个请求/响应消息。这意味着可以建立一个连接并使用该连接传输多个资源，而不需要等待响应返回。
        - **二进制分帧**：http/2.0将消息分割成小的二进制帧来传输。这使得服务器和客户端可以更快速和准确地识别和处理消息。
        - **首部压缩**：http/2.0使用了新的首部压缩算法，以减少网络数据传输。这有助于降低延迟和传输所需的带宽。
        - **服务器推送**：http/2.0允许服务器向客户端推送资源，而无需等待客户端请求。
- http/3.0：2021年
    - http/3.0 是一种新的超文本传输协议，旨在提高因网络延迟和阻塞而导致的网站速度的性能，并加强安全性。它的主要优点是使用基于udp的quic协议代替基于tcp的http/2，这允许数据被更快地发送和接收，并且能够**地管理多个请求和响应之间的流，有助于减轻拥堵问题。此外，http/3还使用tls 1.3 作为加密层，以增强传输数据的安全性。

## 回到问题本质，HTTP 是什么？

HTTP 是*超文本传输协议*，英文名为**H**yper**T**ext **T**ransfer **P**rotocol。

> 概念：是一种用于在互联网上传输超文件的通信协议。它是客户端与服务器之间通讯时使用的一种约定，用于规定请求和响应报文的格式、内容和意义。
> 

拆解这个词，我们可以得到：超文本、传输、协议

### 协议

“协议”指的是**双方通信时约定的标准规则和格式**。就像我们日常生活中人与人签署的合同、签名的协议一样。HTTP 中的协议也是如此，这些规则和格式包括了客户端和服务器之间进行通信的语法、语义以及流程，以确保它们能够相互理解和正确处理请求和响应。

http协议使用计算机可理解的语言来定义计算机之间通信的规范，以及相关的控制和处理错误的方法。更通俗易懂的讲，http协议使得用户在互联网上的web资源传输和交换变得非常容易和高效。如果客户端或服务器不遵守http协议的规范，则可能会导致通信错误或扰乱正常的数据传输过程。

### 传输

在超文本传输协议（HTTP）中，“传输” 指的是客户端（如网页浏览器）与服务器之间的数据传输。更确切地说，它指的是数据的传输方式。

> 简而言之：**传输指的是客户端与服务端之间的数据传递。**
> 

HTTP 中可以采用几种传输类型，包括：

- `chunked`：数据按指定大小分块发送。
- `compress`：数据在发送前先进行压缩。
- `gzip`：使用 gzip 算法对数据进行压缩。
- `identity`：数据按原样发送，不进行编码或压缩。

`传输编码（Transfer-Encoding）`标头用于指定所采用的传输类型。例如，如果服务器使用 gzip 压缩算法发送数据，它会在响应中包含如下标头：

```
Transfer-Encoding: gzip
```

这告知客户端数据是使用 gzip 进行压缩的，客户端在将数据展示给用户之前应当对其进行解压缩。

值得注意的是，`传输编码（Transfer-Encoding）`标头与`内容编码（Content-Encoding）`标头不同，后者用于指定数据本身的编码方式（例如 UTF-8、ISO-8859-1 等）

### 超文本

超“超文本” 一词指的是**包含指向其他文本或资源的超链接的文本**。HTTP（超文本传输协议）是一种用于在互联网上传输数据的协议。在该协议中，超文本指的是包含指向其他资源（如网页、图片、视频以及其他文件）链接的文本。

当用户点击超文本文档中的一个超链接时，就会使用 HTTP 协议向服务器请求所链接的资源。随后服务器会将被请求的资源发送给客户端，客户端可以将其展示出来或以其他方式加以利用。

实际上，超文本使得网页能够包含指向其他页面、图片、视频以及其他文件的链接。这让用户能够轻松地在网络上的不同资源之间进行浏览切换。

以下是 HTML 中超文本链接的一个示例：

```
<a href="https://www.example.com">Example Website</a>
```

# 总结

## 1. 解释下什么是 HTTP 协议

HTTP 即超文本传输协议，来自英文名 **H**yper**T**ext **T**ransfer **P**rotocol。

- **协议**：用计算机可理解的语言来定义计算机之间通信规范、错误处理等相关控制，使用户在web上的资源交互变得简单高效。
- 是客户端与服务端之间的数据传递。其涵盖多种传输类型，如数据分块发送的 “chunked”、发送前压缩数据的 “compress”、采用 gzip 算法压缩的 “gzip” 以及数据原样发送的 “identity” 等。通过 “传输编码（Transfer-Encoding）” 标头来明确传输类型
- **超文本**：是包含指向其他文本或资源超链接的文本。在 HTTP 协议里，超文本可连接网页、图片、视频等各类资源。用户点击超链接时，HTTP 协议便会向服务器请求对应资源，服务器响应后，客户端可展示或利用这些资源，这极大方便了用户在网络不同资源间的浏览与切换。