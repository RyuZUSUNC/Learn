# level-1
抓包绕过

# level-2
修改数据包 Content-Type字段为 image/png 或者 image/gif

# level-3
扩展后缀名绕过，可以使用如下

phtml，php3，php4, php5, pht

但前提是apache中配置了解析扩展后缀

# level-4
使用 .htaccess 把所有文件都当做php解析

将数据包改为如下样式
```
------WebKitFormBoundaryxDA3nX5ZqPgnuUs4
Content-Disposition: form-data; name="upload_file"; filename=".htaccess"
Content-Type: image/png

SetHandler application/x-httpd-php
------WebKitFormBoundaryxDA3nX5ZqPgnuUs4
Content-Disposition: form-data; name="submit"

涓婁紶
------WebKitFormBoundaryxDA3nX5ZqPgnuUs4--
```

# level-5
大小写绕过，如.phP

# level-6
后缀名加空格绕过，如 `.php `

# level-7
后缀名加 `.` 绕过, 如 `.php.`

# level-8
后缀名加::$DATA绕过，如 `.php::$DATA`

# level-9
后缀名加 `. .` 绕过，如 `.php. .`

# level-10
双写后缀名绕过，如 `.pphphp`

# level-11
`%00` 截断，如 `.php%00.png` 
上传后访问 `.php%00` 就可以截断后面的尾缀

# level-12
在二进制中添加`%00`

# level-13
图片码配合文件包含漏洞解析
```
copy 1.jpg /b + 1.php /a shell.jpg
```

# level-14
可使用13关的图片码绕过

# level-15
可使用10关的绕过

# level-16
下载上传的图片对比，查看哪些地方没有被修改，插入php代码

# level-17
条件竞争

# level-18
条件竞争

# level-19
move_uploaded_file会忽略掉文件末尾的/.
使用 `/.`绕过