# 运行 JSSE 示例代码

该 JSSE 示例程序来说明如何应用 JSSE 到：

* 创建一个客户端和一个服务器之间的安全套接字连接
* 创建一个 HTTPS 网站的安全连接
* 使用与 RMI 安全通信
* 举例说明 SSLEngine 使用

当您使用示例代码，请注意示例程序的目的是演示如何使用JSSE。它们的目标不是设计成强大的应用程序。

**注：**建立安全通信涉及到复杂的算法。示例程序提供了没有反馈的设置过程中。当你运行的程序，要有耐心：您可能看不到了任何输出。如果您用设置程序所有 javax.net.debug 系统属性，你会看到更多的反馈。为了介绍阅读本调试信息，请参阅[调试 SSL/TLS 连接](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/ReadDebug.html)。

### 哪里可以找到示例代码

大部分示例代码位于[示例文档](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/index.html)的同一目录中的示例子目录中。按照该链接以查看所有示例代码文件和文本文件的列表。该页面还提供了一个链接到一个ZIP文件，您可以下载来获取所有的示例代码的文件.

以下部分描述了示例。欲了解更多信息，请参阅[README.txt](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/README.txt)文件。

### 示例代码说明客户端和服务器之间的安全 Socket 连接

在 samples/sockets 目录下的示例程序说明了如何设置客户端和服务器之间的安全 socket 连接。

当运行样本客户端程序，可以与现有的服务器进行通信，例如商业 Web 服务器，也可以与示例服务器程序，ClassFileServer 交互。您可以连接到同一个网络中不同的机器上运行示例客户端和服务器示例程序，也可以在一台机器上，但来自不同的终端窗口中运行它们。

所有 samples/sockets/client 目录下的 SSLSocketClient* 示例（以及 [Sample Code Illustrating HTTPS Connections](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/JSSERefGuide.html#HTTPSSample) 中描述的 URLReader* ）可以与 ClassFileServer 运行。[Running SSLSocketClientWithClientAuth with ClassFileServer](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/JSSERefGuide.html#SSCWCAnCFS) 描述了如何使用这个例子。对 ClassFileServer 做类似的改动来运行 URLReader，SSLSocketClient，或 SSLSocketClientWithTunneling。

如果客户机和服务器之间通信过程中发生了认证错误（无论是使用网络服务器或 ClassFileServer），最有可能的原因是为必要的密钥没有在  truststore（信任密钥数据库）。例如，ClassFileServer 使用一名为testkeys 的 keystore 包含用于 localhost 进行 SSL 握手的私钥 。testkeys keystore 包含在相同的 samples/sockets/server 目录作为 ClassFileServer 源。如果客户端无法找到 localhost 在 truststore 中对应的公钥证书，就会产生验证错误。一定要使用samplecacerts truststore （包含 localhost 的公钥和证书），正如在下一节中所述。

#### 配置要求

运行示例程序，创建一个安全的客户机和服务器之间的连接时，您将需要确保相应的证书文件（truststore）可用。对于客户端和服务器程序，你应该使用 samples 目录的证书文件 samplecacerts。使用该证书文件将允许客户端对服务器进行身份验证。该文件包含了所有常用的 Certificate Authority (CA) 使用 JDK（在 cacerts 文件）的证书，加上一个与 ClassFileServer 通讯时由客户端需要验证 localhost 的证书。Classfileserver 使用包含了 localhost 私钥的 keystore，对应于samplecacerts 的公钥。

为了让 samplecacerts 文件提供给客户端和服务器，你可以将它复制到java-home/lib/security/jssecacerts ，重命名为 cacerts，用它来代替  java-home/lib/security/cacerts 文件，或添在 java 命令行形式加以下选项在 客户端和服务器中：
	
	-Djavax.net.ssl.trustStore=path_to_samplecacerts_file

关于 java-home 的更多信息，参见[JRE安装目录](The JRE Installation Directory/The JRE Installation Directory.md)。

为了让 samplecacerts truststore 密码修改。你可以使用 keytool 工具在你自己的证书示例中。

如果您使用浏览器，如 Netscape Navigator 或微软的IE浏览器，访问ClassFileServer 实例中的 SSL 服务器，然后一个对话框会弹出的消息，说它不承认证书。这是很正常的，因为与示例程序一起使用的证书是自签名的，并且只用于测试。您可以接受当前会话的证书。经过测试SSL服务器，你应该退出浏览器，从浏览器的命名空间删除测试证书。

对于客户端身份验证，一个单独的 duke 证书是在适当的目录中可用。公钥和证书存储在 samplecacerts 文件。

#### 运行 SSLSocketClient

[SSLSocketClient.java](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/sockets/client/SSLSocketClient.java) 程序演示如何创建一个客户端,使用一个 SSLSocket 发送一个 HTTP 请求和从一个 HTTPS 服务器响应。这个项目的输出是 https://www.verisign.com/index.html 的 HTML 源代码。

你不能在提供防火墙保护的情况下运行这个程序，不然会得到一个UnknownHostException，因为 JSSE 通过防火墙访问www.verisign.com 找不到路径。创建一个等效的客户端可以运行在防火墙保护相爱,需要设置代理隧道见，示例程序SSLSocketClientWithTunneling。

#### 运行 SSLSocketClientWithTunneling

[SSLSocketClientWithTunneling.java](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/sockets/client/SSLSocketClientWithTunneling.java) 程序说明了如何实现代理隧道访问一个安全的 web 服务器在防火墙保护下。要运行这个程序,您必须将Java 系统属性设置为适当的值:

	java -Dhttps.proxyHost=webproxy
	-Dhttps.proxyPort=ProxyPortNumber
	SSLSocketClientWithTunneling

**注意:**代理规范使用 -D 选项都是可选的。webproxy 替换为您的代理主机的名称,ProxyPortNumber 代表适当的端口号。

程序将从 https://www.verisign.com/index.html 返回的 HTML 源文件。

#### 运行 ClassFileServer

程序 ClassFileServer 有两个文件: [ClassFileServer.java](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/sockets/server/ClassFileServer.java) 和 [ClassServer.java](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/sockets/server/ClassServer.java)。

运行 ClassFileServer.class,它需要以下参数:

* 端口可以是任何未使用的端口号,例如,您可以使用2001
* docroot 表示服务器上的目录,其中包含您要检索的文件。例如,在Solaris上,您可以使用 /home/userid/(用户标识是指特定的UID),而在Microsoft Windows 系统上,您可以使用 c:\
* TLS 是一个可选参数,表示服务器是使用 SSL 还是 TLS
* true 是一个可选参数,表明客户端身份验证是必须的。这个参数只是在 TLS 参数设置后会咨询

**注意:** TLS和 true 的参数是可选的。如果你忽略他们,这表明这个当作普通(而不是 TLS)文件服务器使用,没有身份验证,什么也不会发生。这是因为一方(客户端)正试图与TLS协商,而另一个(服务器)没有,所以他们不能交互。

**注:**服务器预期是 GET 请求的形式  GET /path_to_file

#### 用 ClassFileServer 运行 SSLSocketClientWithClientAuth 

您可以使用示例程序 [SSLSocketClientWithClientAuth](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/sockets/client/SSLSocketClientWithClientAuth.java)  和 ClassFileServer 设置身份验证通信,客户端和服务器相互验证。您可以运行示例程序在不同的机器上连接到同一个网络,或者你可以在一台机器上用不同的终端窗口或命令提示符窗口运行它们。设置客户端和服务器,执行以下操作:

1.从一台计算机或终端窗口运行程序 ClassFileServer ,如[“运行ClassFileServer”](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/JSSERefGuide.html#RunningCFS)。

2.在另一台计算机或终端窗口运行程序 SSLSocketClientWithClientAuth 。SSLSocketClientWithClientAuth 需要以下参数:

* 主机的主机名是您正在使用运行 ClassFileServer 的机器
* 端口是为 ClassFileServer 指定相同的端口
* requestedfilepath 表明文件的路径,你想从服务器检索。你必须给出这个  /filepath 参数。正斜杠被用作 GET 语句的一部分,无关乎使用运行在什么类型的操作系统。形成的声明如下:

```
"GET " + requestedfilepath + " HTTP/1.0"
```

**注意**:你可以修改其他的 SSLClient* 应用的 GET 命令来连接到本地的运行的 ClassFileServer

### 说明 HTTPS 连接的示例代码

有两个主要JSSE API 来访问安全通信。一种方法是通过一个 socket 级别API 可用于任意安全通信,说明了SSLSocketClient,SSLSocketClientWithTunneling,SSLSocketClientWithClientAuth (有或没有 ClassFileServer )示例程序。

第二者更加简单,方法是通过标准 Java URL API。你可以安全地使用 HTTPS URL协议访问具有支持 SSL web服务器通过或计划使用 java.net.URL 类。
支持HTTPS URL方案在许多常见的浏览器实现,它允许访问安全的通信而无需JSSE提供的socket级别API。

一个示例 URL 是 https://www.verisign.com。

信任和密钥管理实现与特定的 HTTPS URL 环境有关。JSSE 实现提供了一个 HTTPS URL 实现。使用不同的 HTTPS 协议实现,设置 java.protocol.handler.pkgs   [system property](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/JSSERefGuide.html#SystemProps)  包名称。有关详细信息,请参阅 java.net.URL 类文档。

您可以下载 JSSE 示例文件包括两个示例程序演示如何创建一个 HTTPS 连接。这两个示例程序([URLReader.java](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/urls/URLReader.java)  和 [URLReaderWithOptions.java](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/urls/URLReaderWithOptions.java)) 在 samples/urls 目录。

#### 运行 URLReader

([URLReader.java](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/urls/URLReader.java) 程序演示了使用 URL 类访问一个安全的网站。这个程序的输出是 https://www.verisign.com/ 的 HTML 源代码。默认情况下, HTTPS 协议实现包含了 JSSE 的使用。为了使用不同的实现 设置系统属性 java.protocol.handler.pkgs 的值。该值是包含实现的包的名称。

如果您正在运行防火墙后面的示例代码,那么你必须设置 https.proxyHost 和 https.proxyPort 系统属性。例如,要使用代理主机“webproxy”在端口 8080 上,您可以使用 java 命令以下选项:

	-Dhttps.proxyHost=webproxy
	-Dhttps.proxyPort=8080

此外,您可以在代码中设置系统属性，使用 java.lang.System  的  setProperty()。例如,你可以在你的程序包括以下行:

```java
System.setProperty("java.protocol.handler.pkgs", "com.ABC.myhttpsprotocol");
System.setProperty("https.proxyHost", "webproxy");
System.setProperty("https.proxyPort", "8080");
```

#### 运行 URLReaderWithOptions

[URLReaderWithOptions.java](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/urls/URLReaderWithOptions.java) 与 URLReader.java 程序类似,除了它可以允许您选择输入任何或所有下列系统属性作为程序运行时的参数:

* java.protocol.handler.pkgs
* https.proxyHost
* https.proxyPort
* https.cipherSuites

运行  URLReaderWithOptions ，这如下命令：

	java URLReaderWithOptions [-h proxyhost -p proxyport] [-k protocolhandlerpkgs] [-c ciphersarray]

注:多个协议处理程序可以包含在 protocolhandlerpkgs 参数的列表项。多个 SSL 密码套件名称可以包含在 ciphersarray 参数的列表项之间用逗号分隔。可能的密码套件名称使用相同SSLSocket.getSupportedCipherSuites() 方法返回的。套件的名称取自 SSL 和 TLS 协议规范。

你需要一个 protocolhandlerpkgs 参数，只有当你想使用一个 HTTPS 协议处理器实现 Oracle 提供的默认的一个。

如果您正在运行防火墙后面的示例代码,那么您必须包括代理主机和代理端口。此外,您可以启用包括一个密码套件使列表。

这里有一个例子运行 URLReaderWithOptions 并指定代理主机的“webproxy”在端口8080上:

	java URLReaderWithOptions -h webproxy -p 8080

### 示例代码演示创建一个安全的 RMI 连接

samples/rmi 目录中的示例代码演示了如何创建一个安全的  Java Remote Method Invocation (RMI) 连接。示例代码是基于 [RMI 的例子](https://docs.oracle.com/javase/8/docs/technotes/guides/rmi/socketfactory/index.html),基本上是一个“Hello World”示例修改安装和使用一个定制的 RMI socket 工厂。

有关Java RMI的更多信息,请参见[Java RMI文档](https://docs.oracle.com/javase/8/docs/technotes/guides/rmi/index.html)。这个网页指向 Java RMI 相关的 Java RMI 的教程和其他信息。

### 示例代码演示了 SSLEngine 的使用

SSLEngine 给应用程序开发人员灵活性的选择 I/O 和计算策略。而不是把SSL/TLS 实现自一个特定的 I/O 抽象(如单线程 SSLSocket ),SSLEngine 消除了 I/O 和实现自 SSL/TLS的计算约束。

如前所述,SSLEngine 是一种高级的API,不适合日常使用。这里提供一些介绍性的示例代码,帮助说明其使用。第一个演示删除大部分的 I/O 和线程问题,并且关注了许多 SSLEngine 方法。第二个演示是一个更实际的例子展示 SSLEngine 如何结合 Java NIO 创建一个基本的 HTTP/HTTPS 服务器。

#### 运行 SSLEngineSimpleDemo


[SSLEngineSimpleDemo](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/sslengine/SSLEngineSimpleDemo.java) 是一个非常简单的应用程序，关注于 SSLEngine 的操作，用来简化了 I/O 和线程问题。这个应用程序创建两个 SSLEngine 对象 通过常见的ByteBuffer对象来进行 SSL/TLS 消息交换的对象。
单一循环连续执行的所有引擎的操作，并且展示了如何建立一个安全连接(握手),应用程序数据传输,以及如何关闭引擎。

SSLEngineResult 提供了大量的关于 SSLEngine 的当前状态的信息。这个例子不解释所有状态的检查。它简化了 I/O 和线程问题,虽然这不是一个很好的用于生产环境的例子，但它对于演示 SSLEngine 的整体功能非常有用的。

#### 运行基于 NIO 的服务器

为了充分利用 SSLEngine 提供的灵活性,您必须首先了解互补的 API,如I/O 以及线程模型。

一个 I/O 模型,在大规模应用程序中开发人员选择使用 NIO SocketChannel 。NIO 引入就是为了解决 java.net.Socket API 固有的可伸缩性问题。SocketChannel 有许多不同的操作模式,包括:

* 阻塞
* 非阻塞
* 非阻塞选择器

示例代码提供了一个基本的 HTTP 服务器,不仅展示了许多新 NIO API,但也展示出 SSLEngine 可以用来创建一个安全的 HTTPS 服务器。服务器不具备生产的质量,但它确实显示许多这样的新 API。 

在目录下是一个 README.txt 文件,介绍了服务器,解释了如何构建和配置服务器,并提供代码布局的简要概述。 SSLEngine 用户最感兴趣的文件是ChannelIO.java 和 ChannelIOSecure.java。

**注意:**在这一节中讨论的服务器的例子包括在 JDK 中。你可以在 jdk-home/samples/nio/server 目录中找到。