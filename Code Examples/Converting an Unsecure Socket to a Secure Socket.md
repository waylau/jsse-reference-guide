# 将不安全的 Socket 转为安全的 Socket

本节提供的源代码的例子来说明如何使用 JSSE 将不安全的 Socket 连接转为安全的 Socket 连接。本节中的代码摘自本书 Java SE 6 Network Security（Marco Pistoia 等著）。

第一个例子是“没有 SSL 的 Socket 实例”的示例代码，可以使用不安全的 Socket 设置客户端和服务器之间的通信。此代码是在“使用 SSL 的 Socket 实例”上的例子做了修改。

### 没有 SSL 的 Socket 实例

下面是服务器端和客户端建立不安全 socket 连接。

在一个 Java 程序中，作为服务器和客户端使用 socket 交互，建立 socket 通讯类似是以下的代码：

```java
import java.io.*;
import java.net.*;

. . .

int port = availablePortNumber;

ServerSocket s;

try {
    s = new ServerSocket(port);
    Socket c = s.accept();

    OutputStream out = c.getOutputStream();
    InputStream in = c.getInputStream();

    // Send messages to the client through
    // the OutputStream
    // Receive messages from the client
    // through the InputStream
} catch (IOException e) { }
```

客户端使用 socket 来与服务器通讯，代码设置如下：

```java
import java.io.*;
import java.net.*;

. . .

int port = availablePortNumber;
String host = "hostname";

try {
    s = new Socket(host, port);

    OutputStream out = s.getOutputStream();
    InputStream in = s.getInputStream();

    // Send messages to the server through
    // the OutputStream
    // Receive messages from the server
    // through the InputStream
} catch (IOException e) { }
```

### 使用 SSL 的 Socket 实例

下面是服务器端和客户端建立安全 socket 连接。

在一个 Java 程序中，作为服务器和客户端使用安全的 socket 交互，建立 socket 通讯类似是以下的代码：

```java
import java.io.*;
import javax.net.ssl.*;

. . .

int port = availablePortNumber;

SSLServerSocket s;

try {
    SSLServerSocketFactory sslSrvFact =
        (SSLServerSocketFactory)SSLServerSocketFactory.getDefault();
    s = (SSLServerSocket)sslSrvFact.createServerSocket(port);

    SSLSocket c = (SSLSocket)s.accept();

    OutputStream out = c.getOutputStream();
    InputStream in = c.getInputStream();

    // Send messages to the client through
    // the OutputStream
    // Receive messages from the client
    // through the InputStream
}

catch (IOException e) {
}
```

户端使用安全的 socket 来与服务器通讯，代码设置如下：