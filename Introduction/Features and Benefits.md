# 特性和用途

JSSE 包括以下重要的特性:

* 作为一个标准的 JDK 组件
* 可扩展的,基于供应商的架构
* 100% 纯 Java 实现
* 提供了支持SSL版本 2.0 和 3.0,TLS 1.0 和以后版本的API，以及SSL 3.0 、TLS 3.0的实现和
* 包含可以实例化创建安全通道(SSLSocket、SSLServerSocket SSLEngine)的类
* 支持作为 SSL 握手的一部分的密码套件协商,用来启动或验证安全通信
* 支持客户端和服务器身份验证,这是正常的 SSL 握手的一部分
* 支持 HTTP 封装 SSL 协议,它允许使用 HTTPS 访问如 web 页面数据
* 提供服务器会话管理 api 来管理驻留内存的 SSL 会话
* 支持几种加密算法中常用密码套件,其中包括下表中列出的：

Table 1: Cryptographic Functionality Available in JSSE

密码算法[^注1]  | 加密过程 |	密钥长度(字节)
---- | ---- | ----
Rivest Shamir Adleman (RSA)	| 认证和密钥交换 | 512 以及更大Rivest Cipher 4 (RC4) |	批量加密 | 128，128 (40 effective)
Data Encryption Standard (DES) | 批量加密 | 64 (56 effective)，64 (40 effective)
Triple DES (3DES) | 批量加密 | 192 (112 effective)
Advanced Encryption Standard (AES) | 批量加密 |	256[^注2] ，128
Diffie-Hellman (DH) | 密钥协议 | 1024，512
Digital Signature Algorithm (DSA) |	身份验证 | 1024

* [^注1]: SunJSSE 的实现是使用 [JCA](https://docs.oracle.com/javase/8/docs/technotes/guides/security/crypto/CryptoSpec.html) 用于所有的加密算法 
* [^注2]: 密码套件使用 AES_256 需要安装   Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files。 详见 [Java SE下载页面](http://www.oracle.com/technetwork/java/javase/downloads/index.html)。