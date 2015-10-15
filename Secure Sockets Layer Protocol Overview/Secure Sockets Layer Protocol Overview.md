# SSL 协议总览

Secure Sockets Layer (SSL，安全套接字层)是在网络上应用最广泛的加密协议实现。SSL 使用结合加密过程来提供网络的安全通信。本节介绍 SSL 和它所使用的加密过程。

SSL 提供了一个安全的增强标准 TCP/IP 套接字用于网络通信协议。如表3所示,添加了安全套接字层传输层和应用层之间的标准 TCP/IP 协议栈。SSL的应用程序中最常用的是 Hypertext Transfer Protocol (HTTP，超文本传输协议),这个是互联网网页协议。其他应用程序,如  Net News Transfer Protocol (NNTP，网络新闻传输协议)、Telnet、 Lightweight Directory Access Protocol (LDAP，轻量级目录访问协议), Interactive Message Access Protocol (IMAP，互动信息访问协议)和 File Transfer Protocol (FTP,文件传输协议),也可以使用 SSL。

注:目前还没有标准的安全的 FTP。

Table 3: TCP/IP Protocol Stack with SSL

TCP/IP 层	| 协议
---- | ----
Application Layer | HTTP, NNTP, Telnet, FTP, 等
Secure Sockets Layer |	SSL
Transport Layer	| TCP
Internet Layer	| IP

SSL 是由网景公司在 1994 年,来自互联网社区的投入,现在已经演变成为一个标准。现在国际标准组织 Internet Engineering Task Force (IETF)的控制下。IETF 更名为 SSL 为 Transport Layer Security (TLS，传输层安全),在 1999年1月发布了第一个规范,版本1.0。TLS 1.0 对于 SSL 的最新版本 3.0版本 是一个小的升级。SSL 3.0  和 TLS 1.0之间的差异是微小的。TLS 1.1 是在2006年4月发布的,TLS 1.2 在 2008年8月 发布。然而,这些更新的版本并不像 TLS 1.0 和 SSL 3.0 一样广泛支持。