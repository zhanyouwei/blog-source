# what's HTTP2

## What's HTTP

From wikipedia

> **超文本传输协议**（[英文](https://zh.wikipedia.org/wiki/%E8%8B%B1%E6%96%87)：**HyperText Transfer Protocol**，[缩写](https://zh.wikipedia.org/wiki/%E7%B8%AE%E5%AF%AB)：**HTTP**）是[互联网](https://zh.wikipedia.org/wiki/%E7%B6%B2%E9%9A%9B%E7%B6%B2%E8%B7%AF)上应用最为广泛的一种[网络协议](https://zh.wikipedia.org/wiki/%E7%BD%91%E7%BB%9C%E5%8D%8F%E8%AE%AE)。设计HTTP最初的目的是为了提供一种发布和接收[HTML](https://zh.wikipedia.org/wiki/HTML)页面的方法。通过HTTP或者HTTPS协议请求的资源由[统一资源标识符](https://zh.wikipedia.org/wiki/%E7%B5%B1%E4%B8%80%E8%B3%87%E6%BA%90%E6%A8%99%E8%AD%98%E7%AC%A6)（Uniform Resource Identifiers，URI）来标识。

## What's HTTP2

From wikipedia

> **HTTP/2**（超文本传输协议第2版，最初命名为**HTTP 2.0**），是[HTTP](https://zh.wikipedia.org/wiki/HTTP)协议的的第二个主要版本，使用于[万维网](https://zh.wikipedia.org/wiki/%E5%85%A8%E7%90%83%E8%B3%87%E8%A8%8A%E7%B6%B2)。HTTP/2是[HTTP](https://zh.wikipedia.org/wiki/HTTP)协议自1999年HTTP 1.1发布后的首个更新，主要基于[SPDY](https://zh.wikipedia.org/wiki/SPDY)协议。它由[互联网工程任务组](https://zh.wikipedia.org/wiki/%E4%BA%92%E8%81%94%E7%BD%91%E5%B7%A5%E7%A8%8B%E4%BB%BB%E5%8A%A1%E7%BB%84)（IETF）的Hypertext Transfer Protocol Bis（httpbis）工作小组进行开发。该组织于2014年12月将HTTP/2标准提议递交至[IESG](https://zh.wikipedia.org/w/index.php?title=Internet_Engineering_Steering_Group&action=edit&redlink=1)进行讨论，于2015年2月17日被批准。HTTP/2标准于2015年5月以RFC 7540正式发表。

## What's SPDY

From wikipedia

>**SPDY**（发音如英语：speedy），一种[开放](https://zh.wikipedia.org/wiki/%E9%96%8B%E6%94%BE%E5%8E%9F%E5%A7%8B%E7%A2%BC)的[网络传输协议](https://zh.wikipedia.org/wiki/%E7%B6%B2%E8%B7%AF%E5%82%B3%E8%BC%B8%E5%8D%94%E5%AE%9A)，由[Google](https://zh.wikipedia.org/wiki/Google)开发，用来发送网页内容。基于[传输控制协议](https://zh.wikipedia.org/wiki/%E4%BC%A0%E8%BE%93%E6%8E%A7%E5%88%B6%E5%8D%8F%E8%AE%AE)（TCP）的[应用层](https://zh.wikipedia.org/wiki/%E5%BA%94%E7%94%A8%E5%B1%82)协议 。Google最早是在[Chromium](https://zh.wikipedia.org/wiki/Chromium)中提出的SPDY协议。目前已经被用于[Google Chrome](https://zh.wikipedia.org/wiki/Google_Chrome)浏览器中来访问Google的SSL加密服务。SPDY并不是[首字母缩略字](https://zh.wikipedia.org/wiki/%E9%A6%96%E5%AD%97%E6%AF%8D%E7%BC%A9%E7%95%A5%E5%AD%97)，而仅仅是"speedy"的缩写。SPDY现为Google的[商标](https://zh.wikipedia.org/wiki/%E5%95%86%E6%A0%87)。
>
>SPDY当前并不是一个标准协议，但SPDY的开发组已经开始推动SPDY成为正式标准（现为[互联网草案](https://zh.wikipedia.org/w/index.php?title=%E4%BA%92%E8%81%94%E7%BD%91%E8%8D%89%E6%A1%88&action=edit&redlink=1)，[HTTP/2](https://zh.wikipedia.org/wiki/HTTP/2)主要以SPDY技术为主。[Google Chrome](https://zh.wikipedia.org/wiki/Google_Chrome)，[Mozilla Firefox](https://zh.wikipedia.org/wiki/Mozilla_Firefox)，[Opera](https://zh.wikipedia.org/wiki/Opera)和[Internet Explorer](https://zh.wikipedia.org/wiki/Internet_Explorer)[[\]](https://zh.wikipedia.org/wiki/SPDY#cite_note-ie11-5)均已支持SPDY协议。SPDY协议类似于[HTTP](https://zh.wikipedia.org/wiki/HTTP)，但旨在缩短[网页](https://zh.wikipedia.org/wiki/%E7%BD%91%E9%A1%B5)的加载时间和提高安全性。SPDY协议通过压缩、[多路复用](https://zh.wikipedia.org/wiki/%E5%A4%9A%E8%B7%AF%E5%A4%8D%E7%94%A8)和优先级来缩短加载时间。

## Why HTTP2

### 慢

影响一个网络请求的因素主要有两个，带宽和延迟。今天的网络基础建设已经使得带宽得到极大的提升，大部分时候都是延迟在影响响应速度。

### 连接无法复用

连接无法复用会导致每次请求都经历三次握手和慢启动。三次握手在高延迟的场景下影响较明显，慢启动则对文件类大请求影响较大。

### head of line blocking

head of line blocking会导致带宽无法被充分利用，以及后续健康请求被阻塞。

HTTP1.0 -> HTTP1.1

 ![http_pipelining_performance](http://7xs2h9.com1.z0.glb.clouddn.com/blog/http_pipelining_performance.png)

不过pipelining并不是救世主，它也存在不少缺陷：

- pipelining只能适用于http1.1，一般来说，支持http1.1的server都要求支持pipelining


- 只有幂等的请求（GET，HEAD）能使用pipelining，非幂等请求比如POST不能使用，因为请求之间可能会存在先后依赖关系。


- head of line blocking并没有完全得到解决，server的response还是要求依次返回，遵循FIFO(first in first out)原则。也就是说如果请求1的response没有回来，2，3，4，5的response也不会被送回来。


- 绝大部分的http代理服务器不支持pipelining。


- 和不支持pipelining的老服务器协商有问题。


- 可能会导致新的Front of queue blocking问题。





##  HTTP2 VS HTTP1.1

### 多路复用

多路复用通过多个请求stream共享一个tcp连接的方式，解决了http1.x holb（head of line blocking）的问题，降低了延迟同时提高了带宽的利用率。

 ![http-6](http://7xs2h9.com1.z0.glb.clouddn.com/blog/http-6.png)

### 压缩头部

HTTP/2.0规定了在客户端和服务器端会使用并且维护「首部表」来跟踪和存储之前发送的键值对，对于相同的头部，不必再通过请求发送，只需发送一次
事实上,如果请求中不包含首部（例如对同一资源的轮询请求），那么首部开销就是零字节。此时所有首部都自动使用之前请求发送的首部。
如果首部发生变化了，那么只需要发送变化了数据在Headers帧里面，新增或修改的首部帧会被追加到“首部表”。首部表在 HTTP2.0的连接存续期内始终存在,由客户端和服务器共同渐进地更新。

 ![Header复用](http://7xs2h9.com1.z0.glb.clouddn.com/blog/Header%E5%A4%8D%E7%94%A8.png)

### 二进制分帧

在应用层与传输层之间增加一个二进制分帧层，以此达到“在不改动HTTP的语义，HTTP 方法、状态码、URI及首部字段的情况下，突破HTTP1.1的性能限制，改进传输性能，实现低延迟和高吞吐量。”


在二进制分帧层上，HTTP2.0会将所有传输的信息分割为更小的消息和帧,并对它们采用二进制格式的编码，其中HTTP1.x的首部信息会被封装到Headers帧，而我们的request body则封装到Data帧里面。

 ![二进制分帧](http://7xs2h9.com1.z0.glb.clouddn.com/blog/%E4%BA%8C%E8%BF%9B%E5%88%B6%E5%88%86%E5%B8%A7.png)



客户端和服务器可以把HTTP消息分解为互不依赖的帧，然后乱序发送，最后再在另一端把它们重新组合起来。注意，同一链接上有多个不同方向的数据流在传输。客户端可以一边乱序发送stream，也可以一边接收者服务器的响应，而服务器那端同理。

 ![共享连接](http://7xs2h9.com1.z0.glb.clouddn.com/blog/%E5%85%B1%E4%BA%AB%E8%BF%9E%E6%8E%A5.png)

### 请求优先级

多路复用导致所有资源都是并行发送，那么就需要「优先级」的概念了，这样就可以对重要的文件进行先传输，加速页面的渲染。

### 服务器推送

服务器推送是指在客户端请求之前发送数据的机制。

另外有一点值得注意的是，客户端如果退出某个业务场景，出于流量或者其它因素需要取消server push，也可以通过发送RST_STREAM类型的frame来做到。



## HTTP2 实践 

这里使用 Node.js 作为服务器端语言。

### 1. 生成**TLS**证书

如果想要在生产环境中使用HTTP2，那么你可以去[这里](https://letsencrypt.org/)生成一个证书。

如果你仅仅开发环境使用，那么我们可以自己生成一个自签名的TSL证书。

##### 1. 安装OpenSSH

##### 2. 使用OpenSSH生成私钥

`openssl genrsa -des3 -passout pass:1234 -out server.pass.key 2048` 

这里 `1234` 为私钥密码，如果你不想使用密码，则可以去除私钥密码，敲入如下密令：

`openssl rsa -passin pass:x -in server.pass.key -out server.key`

##### 3. 创建 证书签名请求

这里使用无密码私钥，如果使用带密码私钥，只需将`server.key`更换为`server.pass.key`即可，密令如下

`openssl req -new -key server.key -out server.csr`

##### 4. 创建证书

`openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt`



通过以上四个步骤，我们得到了三个文件

1. **server.key** 你的TSL证书私钥
2. **server.csr** 你的TSL证书签名请求
3. **server.crt** 你的TSL证书


### 2. 使用Node.js 创建服务器

##### 安装[node-http2](https://github.com/molnarg/node-http2)模块

`npm install http2`

##### 创建服务器

```javascript
var options = {
  key: fs.readFileSync('./server.key'),
  cert: fs.readFileSync('./server.crt')
};

require('http2').createServer(options, function(request, response) {
  response.end('Hello world!');
}).listen(8080);
```



##### 启动服务器

`node index.js`


##### 使用浏览器访问

`http://localhost:8080`

到此，一个简单的Demo就完成了。




### Demo源码下载

[点击这里](https://github.com/zhanyouwei/HTTP2-NodeJS-Demo)访问完整Demo

https://github.com/zhanyouwei/HTTP2-NodeJS-Demo



### 测试结果对比

![http2test](http://7xs2h9.com1.z0.glb.clouddn.com/http2test.png)

![http1test](http://7xs2h9.com1.z0.glb.clouddn.com/http1test.png)

通过上面两张截图可以发现，使用了HTTP2后，同样的请求，在数据传输大小与速度上都有非常大的提升，几乎可以预见，不久的将来，HTTP2将会大放异彩。