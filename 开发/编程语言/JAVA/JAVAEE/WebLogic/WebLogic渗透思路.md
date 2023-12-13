# WebLogic密码破解
Weblogic中的登录密码会以密文的形式存储在服务器本地，当攻击者已经获得服务器权限后可以直接访问该文件。

```
文件名为：config.xml

文件路径为：./config/config.xml

```

```
<node-manager-username>weblogic</node-manager-username> 
  <node-manager-password-encrypted>{AES}rCKfW/HFK7glAWw64jX5Uf2K9Nwz1mzL0f/4aE9uyt=</node-manager-password-encrypted> 

```

在config文件中的node-manager-username节点记录了webogic用户名，node-manager-password节点记录了密码，其加密方式为AES.

除了在config文件中找到用户名和密码外，在./servers/AdminServer/security/boot.properties文件中用户名和密码都会以密文的形式存储。

获取密文后需要对加密后的密码进行解密，解密文件位于./security/SerializedSystemIni.dat

