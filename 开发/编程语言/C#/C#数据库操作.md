# Mysql/Mariadb
## 连接字符串
类似如下
```C#
string connetStr = "server=192.168.203.130;port=3306;user=root;password=toor; database=Test;charset='utf8'";
```
## MySqlConnection
命名空间：MySql.Data.MySqlClient.MySqlConnection;

返回数据库连接对象，参数字符串。实例化“连接对象”，并打开连接

MySqlConnection MySqlCnt = new MySqlConnection(connectString);
MySqlCnt.Open();
使用完成后，需要关闭“连接对象”

sqlCnt.Close();
## MySqlCommand
