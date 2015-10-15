# 术语和定义

本文档包含如下术语和定义：

### authentication (身份验证)

The process of confirming the identity of a party with whom one is communicating.

确认与人交流的过程中一方的身份。

### cipher suite(密码套件)

A combination of cryptographic parameters that define the security algorithms and key sizes used for authentication, key agreement, encryption, and integrity protection.

通过加密参数的组合来定义的安全算法和密钥大小，用于身份验证、密钥协商、加密和完整性保护。

### certificate（证书）

A digitally signed statement vouching for the identity and public key of an entity (person, company, and so on). Certificates can either be self-signed or issued by a Certificate Authority (CA) â€” an entity that is trusted to issue valid certificates for other entities. Well-known CAs include VeriSign, Entrust, and GTE CyberTrust. X509 is a common certificate format that can be managed by the JDK's keytool.

数字签名的声明用来标识一个实体的身份和公钥(个人,公司,等等)。证书可以是自签名或是一个证书颁发机构(CA) 来颁发。证书是证明其他实体可以信任的有效证件。众所周知的 CA 包括 VeriSign,Entrust, 和 GTE CyberTrust。X509 证书是一种常见的格式,可以由 JDK 的 keytool 管理。

### cryptographic hash function（加密散列函数）

An algorithm that is used to produce a relatively small fixed-size string of bits (called a hash) from an arbitrary block of data. A cryptographic hash function is similar to a checksum and has three primary characteristics: it is a one-way function, meaning that it is not possible to produce the original data from the hash; a small change in the original data produces a large change in the resulting hash; and it does not require a cryptographic key.

这是一个算法,用于从任意的数据块产生一个相对较小的部分固定大小的字符串(称为哈希)。加密散列函数类似于一个校验和,有三个主要特征:它是一种单向函数,这意味着它是不可能产生的原始数据散列,一个小的改变原始数据产生很大的变化产生的散列;它不需要密钥。

### Cryptographic Service Provider（加密服务供应商）

Sometimes referred to simply as provider for short, the Java Cryptography Architecture (JCA) defines it as a package (or set of packages) that implements one or more engine classes for specific cryptographic algorithms. An engine class defines a cryptographic service in an abstract fashion without a concrete implementation.


有时简称为[供应商](https://docs.oracle.com/javase/8/docs/technotes/guides/security/crypto/CryptoSpec.html#ProviderArch),Java Cryptography Architecture (JCA,Java加密体系结构)将它定义为一个包(或一组包)实现一个或多个引擎类特定的加密算法。一个引擎类定义了一个抽象的方式而没有具体实现的加密服务。

### decryption (解密)

See encryption/decryption.

见下面的[加密/解密](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/JSSERefGuide.html#EncrDecr)。

### digital signature（数字签名）

A digital equivalent of a handwritten signature. It is used to ensure that data transmitted over a network was sent by whoever claims to have sent it and that the data has not been modified in transit. For example, an RSA-based digital signature is calculated by first computing a cryptographic hash of the data and then encrypting the hash with the sender's private key.

数字相当于一个手写签名。它用于确保数据在网络上传输声明是由谁发送它,并且确保数据在传输过程中没有被修改。例如,一个基于 RSA 数字签名计算,首先计算密码散列的数据,然后用发送方的私钥加密散列。

### encryption/decryption（加密/解密）

Encryption is the process of using a complex algorithm to convert an original message (cleartext) to an encoded message (ciphertext) that is unintelligible unless it is decrypted. Decryption is the inverse process of producing cleartext from ciphertext.

The algorithms used to encrypt and decrypt data typically come in two categories: secret key (symmetric) cryptography and public key (asymmetric) cryptography.

加密的过程中使用复杂的算法来将一个原始消息(明文)转为编码信息(密文),除非它是解密不然编码信息是不可识别的。解密是从密文生成明文的逆过程。

算法用于加密和解密数据通常有两类:密钥(对称)加密和公钥(不对称)加密。

### handshake protocol（握手协议）

The negotiation phase during which the two socket peers agree to use a new or existing session. The handshake protocol is a series of messages exchanged over the record protocol. At the end of the handshake, new connection-specific encryption and integrity protection keys are generated based on the key agreement secrets in the session.

协商阶段期间,两个套接字对同意使用新的或现有的会话。握手协议是一系列交换记录协议的消息。握手结束的时候,新的特定的连接加密和完整性保护密钥的生成是基于会话中的密钥协商密钥。

### key agreement（密钥协商）

A method by which two parties cooperate to establish a common key. Each side generates some data, which is exchanged. These two pieces of data are then combined to generate a key. Only those holding the proper private initialization data can obtain the final key. Diffie-Hellman (DH) is the most common example of a key agreement algorithm.

一个双方合作的方法来建立一个共同的密钥。每一方生成一些数据,并进行交换。这些两个数据会结合生成一个密钥。只有那些持有适当的私人初始化数据可以获得最后的密钥。Diffie-Hellman (DH) 是密钥协议算法最常见的例子。

### key exchange（密钥交换）

A method by which keys are exchanged. One side generates a private key and encrypts it using the peer's public key (typically RSA). The data is transmitted to the peer, who decrypts the key using the corresponding private key.


密钥交换的一种方法。一方生成私钥,并使用对等的公钥加密它(通常是RSA)。数据传输到对等端,使用相应的私钥解密这个密钥。

### key manager/trust manager（密钥管理器/信任管理器）

Key managers and trust managers use keystores for their key material. A key manager manages a keystore and supplies public keys to others as needed (for example, for use in authenticating the user to others). A trust manager decides who to trust based on information in the truststore it manages.

密钥管理器和信任管理器使用 keystore 作为密钥的原料。密钥管理器管理 keystore 并根据需要向他人提供公钥(例如,用于验证用户)。信任管理器基于 truststore 的信息来决定谁是可以信任的。

### keystore/truststore

keystore is a database of key material. Key material is used for a variety of purposes, including authentication and data integrity. Various types of keystores are available, including PKCS12 and Oracle's JKS.

keystore 是一个数据库的密钥材料。密钥材料是用于各种各样的用途,包括身份验证和数据的完整性。有各种类型的 keystores 可用的,包括PKCS12 和 Oracle JKS。

Generally speaking, keystore information can be grouped into two categories: key entries and trusted certificate entries. A key entry consists of an entity's identity and its private key, and can be used for a variety of cryptographic purposes. In contrast, a trusted certificate entry contains only a public key in addition to the entity's identity. Thus, a trusted certificate entry cannot be used where a private key is required, such as in a javax.net.ssl.KeyManager. In the JDK implementation of JKS, a keystore may contain both key entries and trusted certificate entries.

一般来说,keystore 信息可以分为两类:密钥条目和可信任证书条目。一个密钥条目包含一个实体的身份和其私钥,而且可以用于各种加密的目的。相比之下,一个受信任的证书条目除了实体的身份只包含公钥。因此,不能使用可信证书条目,私钥是必需的,比如 javax.net.ssl.KeyManager。JDK 实现 JKS,keystore 可能只包含密钥条目和可信任证书条目。

A truststore is a keystore that is used when making decisions about what to trust. If you receive data from an entity that you already trust, and if you can verify that the entity is the one that it claims to be, then you can assume that the data really came from that entity.

一个 truststore 也是一个 keystore, 作用是决定什么是值得信任。如果你从一个实体已经接收数据,你已经信任了,如果你能确认该实体就是它声称是那个,那么你可以假定的数据来自那个实体。

An entry should only be added to a truststore if the user trusts that entity. By either generating a key pair or by importing a certificate, the user gives trust to that entry. Any entry in the truststore is considered a trusted entry.

一个条目只能是该用户信任的实体才能被添加 truststore。通过生成一个密钥对或通过导入证书,用户给予该条目以信任。信任存储库中的任何条目被认为是一个值得信赖的条目。

It may be useful to have two different keystore files: one containing just your key entries, and the other containing your trusted certificate entries, including CA certificates. The former contains private information, whereas the latter does not. Using two files instead of a single keystore file provides a cleaner separation of the logical distinction between your own certificates (and corresponding private keys) and others' certificates. To provide more protection for your private keys, store them in a keystore with restricted access, and provide the trusted certificates in a more publicly accessible keystore if needed.

有两个不同的 keystore 文件:一个包含只是你的密钥条目,另外一个包含你信任的证书条目,包括 CA 证书。前者包含私人信息,而后者没有。使用两个文件代替单个 keystore 文件提供了一个更整洁的分离的逻辑区别自己的证书(和相应的私钥)和其他人的证书。为了提供更多保护私匙,将它们存储在有访问限制的 keystore 里面,并在需要的时候可以提供更公开访问 keystore 的可信证书。

### message authentication code (MAC) 消息身份验证代码

Provides a way to check the integrity of information transmitted over or stored in an unreliable medium, based on a secret key. Typically, MACs are used between two parties that share a secret key in order to validate information transmitted between these parties.

提供了一种基于密钥方法来检查信息传输或存储在一个不可靠的介质的完整性。通常,使用两方之间的 MAC 来共享一个密钥来验证这些双方之间的信息传输。

A MAC mechanism that is based on cryptographic hash functions is referred to as HMAC. HMAC can be used with any cryptographic hash function, such as Message Digest 5 (MD5) and Secure Hash Algorithm (SHA), in combination with a secret shared key. HMAC is specified in RFC 2104.

MAC 机制是基于加密散列函数称为 HMAC。HMAC 可用于任何的加密散列函数，如 Message Digest 5 (MD5，消息摘要5) 和 Secure Hash Algorithm (SHA，安全散列算法),结合一个秘密共享密钥。HMAC 在 RFC 2104 中指定。

### public-key cryptography 公开密钥加密

A cryptographic system that uses an encryption algorithm in which two keys are produced. One key is made public, whereas the other is kept private. The public key and the private key are cryptographic inverses; what one key encrypts only the other key can decrypt. Public-key cryptography is also called asymmetric cryptography.

加密系统使用加密算法的生成两个密钥。一个密钥是公开,而另一个是私有的。公钥和私钥是加密逆;一个密钥加密只有另一个密钥才能解密。公开密钥加密也被称为非对称加密。

### Record Protocol 记录协议

A protocol that packages all data (whether application-level or as part of the handshake process) into discrete records of data much like a TCP stream socket converts an application byte stream into network packets. The individual records are then protected by the current encryption and integrity protection keys.

协议包的所有数据(应用程序级还是握手过程的一部分)转变成离散的数据记录，就像一个 TCP 流套接字转化成应用程序字节流到网络数据包。独立的记录被当前的加密和完整性保护密钥保护。

### secret-key cryptography 密钥加密

A cryptographic system that uses an encryption algorithm in which the same key is used both to encrypt and decrypt the data. Secret-key cryptography is also called symmetric cryptography.

使用的加密算法的加密系统都使用相同的密钥来加密和解密数据。密钥加密技术也称为对称加密。

### session 会话

A named collection of state information including authenticated peer identity, cipher suite, and key agreement secrets that are negotiated through a secure socket handshake and that can be shared among multiple secure socket instances.

命名的状态信息集合包括验证对等身份,密码套件和密钥协商，主要通过安全套接字协议的秘密握手来协商,可以在多个安全套接字实例之间共享。

### trust manager 信任管理器

See key manager/trust manager.

见 密钥管理器/信任管理器

### truststore

See keystore/truststore.

见 keystore/truststore