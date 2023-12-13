# 网络请求
## requests模块
- pip install requests

```
import requests
```

- import requests后运行脚本文件，如果报错如下openssl相关的信息，则重新安装pyOpenSSL即可。
```
1 AttributeError: cffi library '_openssl' has no function, constant or global variable named 'Cryptography_HAS_NETBSD_D1_METH'
```

### GET请求
- get请求：res = requests.get(url,data=data,cookies=cookie,headers=header,verify=False,files=file)　
  　
  - data可传可不传，data是字典格式。
  - 如果url是https的话，加上verify=False。如果url是http的话，可不加。

```py
import requests

url='http://127.0.0.1:8999/api/login'
data = {'username':'testuser1','passwd':'111111'}
r = requests.get(url,params=data) #发get请求
print(r)#返回<Response [200]>
print(r.json())#将返回的json串转为字典
print(r.text)#返回get到的页面的返回数据

```

### POST请求
- res = requests.post(url,data=data,cookies=cookie,headers=header,verify=False,files=file)　　
  - data是字典格式
  
- res = requests.post(url,json=data,cookies=cookie,headers=header,verify=False,files=file)　
  - data是json格式
  
- Cookie、header里面只能放String 类型的键值对。不能是json格式
- file是二进制文件
- 如果url是https的话，加上verify=False。如果url是http的话，可不加。

```py
import  requests
## --------------------------------------------------------------------
## 发送post请求--带参数（json格式）
## --------------------------------------------------------------------
url3= 'http://127.0.0.1/api/user/add_stu'
data = {"name":"request_name","grade":"3","sex":"男","age":28,"addr":"河南省"}
res = requests.post(url3,json=data)#注意，这里的data是字典格式！之所以json=data，是因为请求报文要求入参是json格式，requests模块会自己将data字典转成json格式再发送请求
print(res)
print(res.json())
print(res.text)
```

### 带cookie（仅字典格式）
如果自定义header中定义了cookies那么此处设置的cookies不生效
```py
import  requests
#获取cookie值
url= 'http://127.0.0.1/api/user/login'
data = {'username':'testuser1','passwd':'111111'}
res = requests.post(url,data=data)
result = res.json()
print(result)
sign = result.get('login_info').get('sign')
## --------------------------------------------------------------------
## 发送cookie
## --------------------------------------------------------------------
url4= 'http://127.0.0.1/api/user/gold_add'
data = {'stu_id':15,'gold':1000}
cookie ={'testuser1':sign}
res = requests.post(url4,data=data ,cookies=cookie)#data是字典
print(res)
print(res.json())
print(res.text)
```

### 带header（仅字典格式）
```py
import  requests
## --------------------------------------------------------------------
## 发送header
## --------------------------------------------------------------------
url5 = 'http://127.0.0.1/api/user/all_stu'
header = {'Referer':'http://api.nnzhp.cn/'}
res = requests.get(url5,headers=header)#传header
print(res)
print(res.json())
print(res.text)
res = requests.get(url5)#不传header
print(res.json())
```

### 带file（仅二进制格式）
```py
import requests
## --------------------------------------------------------------------
## 上传文件
## --------------------------------------------------------------------
url7 = 'http://127.0.0.1/api/file/file_upload'
data = {'file':open('魔鬼中的天使.mp3','rb')}
res = requests.post(url7,files=data)#如果是https的话，要加上verfiy=False参数
print(res.json())
```

### 使用代理
```py
import requests

url='http://docs.python-requests.org/en/master/'
proxies={
    'http':'127.0.0.1:8080',
    'https':'127.0.0.1:8080'
}
r = requests.get(url,proxies=proxies)
print(r.status_code)
```

**socks代理**
python -m pip install Pysocks
```py
import socket

socks.set_default_proxy(socks.SOCKS5, "127.0.0.1", 1081)
socket.socket = socks.socksocket
```

### 会话保执
经常很多请求只有在登录后才能进行，实现登录效果一般的做法是执行登录请求，然后从返回结果中提取sessionid放入自定义cookie中。

这种方法在requests中也行得通，但requests提供了更为简单的方法，直接使用request.Session类来请求即可，其保持登录的原理是保留之前请求中服务端通过set-cookie等设置的参数。

```py
s = Session()
url='http://docs.python-requests.org/en/master/'
# 所有方法和直接使用requests时一样用即可
s.get(url)
```

### 获取响应结果
- res　　#返回如<Response [200]>

- res.status_code  #返回状态码，如200

```py
import requests
## --------------------------------------------------------------------
## 返回状态码
## --------------------------------------------------------------------
url = 'http://www.nnzhp.cn'
res = requests.get(url)#发送get请求
print(res.status_code)#获取状态码
```

- res.json()　　#返回字典。不需要手动decode()转码。如果res结果是json格式，可以使用json()将json串转成字典格式。如果res结果不是json的话，不能使用json()

- res.text　#返回字符串，响应的源码。不能用于下载文件。

- res.content　　#返回二进制。主要用于流媒体文件、图片文件的下载。

#### 下载mp3
```py
import requests
## --------------------------------------------------------------------
## 返回二进制--流媒体
## --------------------------------------------------------------------
url6 = 'http://qiniuuwmp3.changba.com/1084511584.mp3'
res = requests.get(url6)
with open('魔鬼中的天使.mp3','wb') as fw:#把二进制文件下载下来，写入到'魔鬼中的天使.mp3'
    fw.write(res.content)#res.content返回结果是二进制的,如x03\xe3\xa3\xf2......
```

#### 下载图片
```py
import requests
## --------------------------------------------------------------------
## 返回二进制--图片
## --------------------------------------------------------------------
url7 = 'https://aliimg.changba.com/cache/photo/855e5493-f018-44db-8892-c8660649327b_640_640.jpg'
res = requests.get(url7,verify=False)#如果是https的话，要加上verfiy=False参数
print('3.3=====',res.content)#返回结果是二进制的
with open('photo.jpg','wb') as fw:#把二进制文件下载下来，写入到'photo.jpg'
    fw.write(res.content)
```

- res.headers　　#返回响应的所有headers

```py
## --------------------------------------------------------------------
## 返回headers
## --------------------------------------------------------------------
url = 'http://www.nnzhp.cn'
res = requests.get(url)#发送get请求
print(res.headers)#获取所有cookies
```

- res.cookies　　#返回响应的所有cookies

```py
import requests
## --------------------------------------------------------------------
## 返回cookie
## --------------------------------------------------------------------
url = 'http://www.nnzhp.cn'
res = requests.get(url)#发送get请求
print(res.cookies)#获取所有cookies
```
- res.status_code   #返回响应值

# 字符串编码检测
## chardet模块

# 系统运行监测
## psutil模块

# 多项目虚拟环境
## virtualenv

# 音频文件处理
## mutagen