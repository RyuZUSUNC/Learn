#  网速测试
F》https://www.jokeo.cn/540.html

Speedtest.net提供一个命令行版本——speedtest-cli，能够在终端中简单快速的测试出linux的网速

```
wget https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py

chmod a+rx speedtest.py

mv speedtest.py /usr/local/bin/speedtest-cli

chown root:root /usr/local/bin/speedtest-cli

speedtest-cli
```

## Mbit 等于多少 Mbp
换算公式：
```
8bit(位)=1Byte(字节)
1024Byte(字节)=1KB
1024KB=1MB
1024MB=1GB
1024GB=1TB
```

由以上公式可以看出位和字节的比例为8:1
所以要用Mbit得出Mbps，只需要用Mbit除以8即可。

例子：
```
100Mbit / 8 = 12.5Mbp
即：100Mbit/s == 12.5Mbp/s（12.5M/s）
```


