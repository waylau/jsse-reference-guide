# JRE 安装目录

java-home 变量占位符的使用是为了引用  Java Runtime Environment (JRE，Java运行时环境) 的安装目录。这个目录的确认是基于有或没有安装 JDK 的 JSSE 的运行来判断的。JDK 包括 JRE,但位于不同的文件层次结构中。

java-home 的默认位置如下表：

操作系统 | JDK | JRE
---- | ---- | ----
Solaris/Linux |	~/jdk1.8.0/jre	| ~/jre1.8.0
Windows  | C:\jdk1.8.0\jre	| C:\jre1.8.0

**注：**在路径名的波浪线 (~)  是代表在 Solaris，Linux 或 Mac OS X操作系统的当前用户的主目录。