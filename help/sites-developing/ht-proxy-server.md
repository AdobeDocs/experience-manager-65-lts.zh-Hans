---
title: 如何使用代理服务器工具
description: 代理服务器充当在客户端和服务器之间中继请求的中间服务器
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
exl-id: e33640ba-6039-4057-8942-b4faa9b2e250
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---

# 如何使用代理服务器工具{#how-to-use-the-proxy-server-tool}

代理服务器充当在客户端和服务器之间中继请求的中间服务器。 代理服务器跟踪所有客户端 — 服务器交互并输出整个TCP通信的日志。 这使您能够准确地监视正在发生的情况，而无需访问主服务器。

您可以在AEM安装中找到代理服务器，网址为：

`crx-quickstart/opt/helpers/proxy-2.1.jar`

您可以使用代理服务器监视所有客户端 — 服务器交互，而不管底层通信协议如何。 例如，可以监视以下协议：

* 网页的HTTP
* 用于安全网页的HTTPS
* 电子邮件的SMTP
* 用于用户管理的LDAP

例如，您可以在通过TCP/IP网络通信的任意两个应用程序(例如Web浏览器和AEM)之间放置代理服务器。 这样，您就可以监控在请求CQ页面时确切发生的情况。

## 启动代理服务器工具 {#starting-the-proxy-server-tool}

在命令行中启动服务器：

`java -jar proxy-2.1.jar <host> <remoteport> <localport> [options]`

**参数**

`<host>`

这是您要连接到的CRX实例的主机地址。 如果实例位于本地计算机上，则这是`localhost`。

`<remoteport>`

这是目标CRX实例的主机端口。 例如，新安装的AEM安装的默认值为&#x200B;**`4502`**，新安装的AEM创作实例的默认值为`4502`。

`<localport>`

这是您希望连接的本地计算机上的端口，以便通过代理访问CRX实例。

**选项**

`-q` （安静模式）

不将输出写入控制台窗口。 如果不想减慢连接速度，或者将输出记录到文件（请参见 — logfile选项），则使用此选项。

`-b`（二进制模式）

如果您要在流量中查找特定的字节组合，请启用二进制模式。 然后，输出将包含十六进制和字符输出。

`-t` （时间戳日志条目）

向每个日志输出添加时间戳。 时间戳以秒为单位，因此它可能不适合检查单个请求。 如果您使用代理服务器的时间较长，则使用它来查找在特定时间发生的事件。

`-logfile <filename>`（写入日志文件）

将客户端 — 服务器对话写入日志文件。 此参数还可在安静模式下使用。

**`-i <numIndentions>`**（添加缩进）

每个活动连接都进行缩进，以提高可读性。 默认级别为16。 此功能已在`proxy.jar version 1.16`中引入。

### 日志格式 {#log-format}

proxy-2.1.jar生成的日志条目都具有以下格式：

`[timestamp (optional)] [Client|Server]-[ConnectionNumber]-[BytePosition] ->[Character Stream]`

例如，对网页的请求可能如下所示：

`C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]`

* C表示此条目来自客户端（这是对网页的请求）
* 0是连接数（连接计数器从0开始）
* 选#00000字节流中的偏移量。 这是第一个条目，因此偏移为0。
* `[GET <?>]`是请求的内容，例如某个HTTP标头(url)。

当连接关闭时，将记录以下信息：

```
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

这显示第六次连接中客户端(`C`)与服务器(`S`)之间以平均速度传递的字节数。

**日志输出示例**

例如，假定一个页面在请求时生成以下代码：

### 示例 {#example}

例如，假定存储库中的简单html文档位于

`/content/test.html`

图像文件位于

`/content/test.jpg`

`test.html`的内容是：

```xml
<html>
<head>
    <title>Test</title>
</head>
<body>
    Test<br>
    <img src="test.jpg">
</body>
</html>
```

假设AEM实例正在`localhost:4502`上运行，代理的启动方式如下：

`java -jar proxy.jar localhost 4502 4444 -logfile test.log`

现在可以通过`localhost:4444`上的代理访问CQ/CRX实例，通过此端口的所有通信都记录到`test.log`。

如果您现在查看代理的输出，则会看到浏览器与AEM实例之间的交互。

启动时，代理输出以下内容：

```xml
starting proxy for localhost:4502 on port 4444
using logfile: <some-dir>/crx-quickstart/opt/helpers/test.log
```

现在，打开浏览器并访问测试页面：

`http://localhost:4444/content/test.html`

您会看到浏览器对该页面发出`GET`请求：

```shell
C-0-#000000 -> [GET /content/test.html HTTP/1.1 ]
C-0-#000033 -> [Host: localhost:4444 ]
C-0-#000055 -> [Connection: keep-alive ]
C-0-#000079 -> [User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_4) AppleWebKit/536.11 (KHTML, like Gecko) Chrome/20.0.1132.57 Safari/536.11 ]
C-0-#000212 -> [Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8 ]
C-0-#000285 -> [Accept-Encoding: gzip,deflate,sdch ]
C-0-#000321 -> [Accept-Language: en-US,en;q=0.8 ]
C-0-#000354 -> [Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.3 ]
C-0-#000402 -> [Cookie: login-token=179ba6bd-e0a7-4909-a965-e11c7f2bc2fc%3a618bd8a8-fbaf-43c5-827d-c84c62248c5e_22ee860cc9036fee%3acrx.default%3b21148fb0-eb6c]
C-0-#000543 -> [-43c9-a2b9-c8d40618d8ae%3ad87a3d1a-5e9a-4d5a-bab1-0ee60ad6d8df_d0e4ddce0fcd84b6%3acrx.default%3b5cb95227-ea51-47bf-850b-68ad1dfd7297%3af3bbb6]
C-0-#000684 -> [59-7913-4285-8857-832c087bafd5_c484727d3b3665ad%3acrx.default; ys-cq-siteadmin-tree=o%3Awidth%3Dn%253A240%5EselectedPath%3Ds%253A/content ]
C-0-#000824 -> [ ]
```

AEM实例使用文件`test.html`的内容进行响应：

```shell
S-0-#000000 -> [HTTP/1.1 200 OK ]
S-0-#000017 -> [Connection: Keep-Alive ]
S-0-#000041 -> [Server: Day-Servlet-Engine/4.1.24  ]
S-0-#000077 -> [Content-Type: text/html;charset=utf-8 ]
S-0-#000116 -> [Content-Length: 104 ]
S-0-#000137 -> [Date: Mon, 16 Jul 2012 11:23:38 GMT ]
S-0-#000174 -> [Last-Modified: Mon, 16 Jul 2012 11:19:27 GMT ]
S-0-#000220 -> [ ]
S-0-#000222 -> [<html>]
S-0-#000229 -> [<head>]
S-0-#000236 -> [    <title>Test</title>]
S-0-#000260 -> [</head> ]
S-0-#000269 -> [<body>]
S-0-#000276 -> [ Test<br>]
S-0-#000286 -> [    <img src="test.jpg">]
S-0-#000311 -> [</body>]
S-0-#000319 -> [</html>]
```

### 代理服务器的使用 {#uses-of-the-proxy-server}

以下场景说明了可以使用代理服务器的几个目的：

**检查Cookie及其值**

以下日志条目示例显示了自代理启动以来在第六个连接上由客户端发送的所有Cookie及其值：

`C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]`

**检查标头及其值**

以下日志条目示例显示服务器能够建立保持活动连接并且内容长度标头设置正确：

```
S-7-#000017 -> [Connection: Keep-Alive ]
 ...
 S-7-#000107 -> [Content-Length: 124 ]
```

**检查保持活动状态是否有效**

保持活动状态是HTTP的一项功能，它允许客户端重复使用与服务器的TCP连接来发出多个请求（针对页面代码、图片、样式表等）。 如果没有保持活动状态，客户端必须为每个请求建立新的连接。

要检查保持活动状态是否有效，请执行以下操作：

* 启动代理服务器。
* 请求一个页面。
* 如果keep-alive运行正常，则连接计数绝不能超过5到10个连接。
* 如果保持活动不工作，则连接计数迅速增加。

**查找丢失的请求**

如果在复杂的服务器设置中丢失请求，例如，在防火墙和Dispatcher中，您可以使用代理服务器查找请求丢失的位置。 如果有防火墙：

* 在防火墙之前启动代理
* 在防火墙后启动另一个代理
* 使用这些量度可查看请求到达的距离。

**请求挂起**

如果您偶尔遇到挂起的请求：

* 启动代理。
* 等待或将访问日志写入文件，每个条目都具有时间戳。
* 当请求开始挂起时，您可以看到打开了多少连接，以及哪个请求导致了问题。
