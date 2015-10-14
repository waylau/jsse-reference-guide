# 引言

数据在网络上传播很容易被不是预期的收件人进行访问。当数据包含私人信息，如密码和信用卡号码，必须采取措施，以保证使数据不容易透露给未经授权的第三方。同样重要的是，在传输过程中要确保数据没有被修改（有意或无意地）。 Secure Sockets Layer (SSL，安全套接字层)和Transport Layer Security (TLS，传输层安全)协议，旨在保护数据在网络传输的过程中的保密性和完整性。

Java Secure Socket Extension (JSSE，Java 安全套接字扩展) 实现了安全的互联网通信。它提供了一个框架，并为执行 SSL 和 TLS 协议的Java 版本的实现，包括数据加密，服务器认证，消息完整性和可选的客户端认证功能。使用 JSSE，开发者可以提供一个客户端和运行任何基于 TCP/IP 上的应用协议（如 HTTP，Telnet 或 FTP）的服务器之间的数据安全通道。关于 SSL 的更多介绍，请参阅 [SSL 协议总览](../Secure Sockets Layer Protocol Overview/Secure Sockets Layer Protocol Overview.md)。

通过抽象复杂的底层安全算法和握手机制，JSSE 减少创造微妙而危险的安全漏洞的风险。此外，作为一个模块，开发人员可以直接集成它到他们的应用程序简化了应用程序的开发。

JSSE 提供了一个应用程序接口（API）的框架和该 API 的实现。该 JSSE API 补充了核心网络，并通过 java.security 和 java.net 包中提供的扩展的网络套接字类，如信任管理，密钥管理器，SSL 上下文和用于定义的加密服务、套接字工厂框架来封装套接字创建行为。因为 SSLSocket 类是基于阻塞 I/O 模型，Java 开发工具包（JDK）包括一个非阻塞的SSLEngine 类，来选择实现适合自己的 I/O 方法。

该 JSSE API 能够支持 SSL 2.0 和 3.0 版和 TLS 1.0 版。这些安全协议封装一个正常的双向流套接字和 JSSE API 增加了认证，加密和诚信保障的支持。 JSSE 跟 JDK 实现了支持 SSL 3.0 和 TLS 1.0。它不实现SSL 2.0。

JSSE 是 Java SE 平台的安全组件，并且在其他基于 [Java Cryptography Architecture (JCA，基于 Java 加密体系结构）](https://docs.oracle.com/javase/8/docs/technotes/guides/security/crypto/CryptoSpec.html#Design)框架找到相同的设计原则。该框架加密技术有关的安全组件可以让他们实现独立，并尽可能的实现算法独立。 JSSE 使用由 JCA 框架中定义的[加密服务供应商](https://docs.oracle.com/javase/8/docs/technotes/guides/security/crypto/CryptoSpec.html#ProviderArch)。

在 Java SE 平台的其他安全组件包括 [Java Authentication Authorization Service (JAAS，Java认证和授权服务)](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) 和 [Java Security Tools （Java安全工具）](https://docs.oracle.com/javase/8/docs/technotes/tools/index.html#security)。 JSSE 包含许多相同的概念和算法的 JCA 但自动适用于下面一个简单的流套接字 API。

该 JSSE API 的目的是让其他的 SSL/TLS 协议，公钥基础设施（PKI）实现无缝的插入。开发者也可以提供替代的逻辑来确定是否远程主机应信任什么或验证密钥材料是否应该被发送到远程主机。