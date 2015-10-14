# SunJSSE 供应商

Oracle  的 Java SE 的 JSSE 实现是包含了一个名为 SunJSSE 的供应商，通过 JCA 来预装和预注册。这个供应商提供以下加密服务:

* SSL 3.0 和 TLS 1.0 安全协议的实现
* 最常见 SSL 和 TLS 密码套件的实现,其中包括认证、密钥协议、加密和完整性保护
* 一个基于 x.509 的密钥管理器的实现,用于从标准的 JCA keystore 中选择合适的认证密钥
* 一个基于 x.509 的基于信任管理器的实现，用于证书链路径验证规则
* PKCS12 实现了  JCA keystore 类型 "pkcs12"。PKCS12 不支持存储信任锚。用户应该存储信任锚在 Java keystore(JKS) 格式并保存私钥为 PKCS12 格式。

更多关于这个提供者的信息可见 [SunJSSE](https://docs.oracle.com/javase/8/docs/technotes/guides/security/SunProviders.html#SunJSSEProvider) 文档

