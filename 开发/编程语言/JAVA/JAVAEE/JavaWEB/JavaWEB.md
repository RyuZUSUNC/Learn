# 三大组件
- Servlet : 处理请求
- Filter : 过滤/拦截请求
- Listener : 监听器

三大组件基本都需要在web.xml中进行注册:除了Listener中的两个(活化钝化监听器，绑定解绑监听器)

# Filter

配置示例
```xml
<filter>
    <filter-name>MyFirstFilter</filter-name>
    <filter-class>com.ffffffff0x.filter.MyFirstFilter</filter-class>
</filter>

<filter-mapping>
    <filter-name>MyFirstFilter</filter-name>
    <url-pattern>/*<url-pattern>
</filter-mapping>
```

## url-pattern的三种写法
1. 精确匹配
   - 直接拦截指定路径
     - /pics/sa.jsp  
     - /hello/login
2. 路径匹配(模糊匹配)
   - /pics/*
     - 拦截pics写的所有请求
3. 后缀匹配(模糊匹配)
   - *.jsp
     - 拦截所有以.jsp结尾的请求

/pics/*.jsp ：不能这么写

## Filter原理
```java
doFilter(){
    //放行请求;
    chain.doFilter(request,response);
}
```
多个Filter输出流程
![Filter流程](.\img\Filter流程.png)

# Listener
8个listener

- ServletRequest(2个)
  - 生命周期监听器
  - 属性变化监听器
- ServletContext(4个)
  - 生命周期监听器
  - 属性变化监听器
  - 活化钝化监听器
  - 绑定解绑监听器
- ServletContext(2个)
  - 生命周期监听器
  - 属性变化监听器

需要掌握 ServletContextListener:(生命周期监听器)：监听ServletContext的创建和销毁(监听服务器的启动,停止)；服务器启动为当前项目创建ServletContext对象，服务器停止销毁创建的ServletContext

ServletContext
- 一个WEB项目对应一个ServletContext，它代表当前WEB项目的信息
- 还可以作为最大的域对象在整个项目运行期间共享数据

使用方法
1. 实现对应的监听器接口
2. 去web.xml中进行配置
   - 注意:有两个Listener是javaBean需要实现的接口(HttpSessionActivitionListener,HttpSessionBindingListener)

# JSON
JSON JavaScript Object Notation:(js对象表示法)是一种轻量级(和XML相比)的数据交换格式

{key:value,key:value}

value可以有很多种
1. 基本类型(字符串，数字，布尔)
2. 数组
   1. {lastname:"123",books:["11","22"]}

```json
var student = {lastName:"san",age:"12",car:{pp:"1q",price:"123$"},infos:[{bookName:"qwe",price:"12"}]，19}
```

JSON应该是利于传输的字符串

JS方法:
- JSON.stringify() :将JSON对象转换为JSON字符串
- JSON.parse() ：将JSON字符串转换为JSON对象

# AJAX
AJAX即“Asynchronous Javascript And XML" (异步JavaScript和XML)
- AJAX是一种无刷新页面与服务器的交互技术:(页面不刷新就可以收到服务器响应的数据)

原来的交互

- 发送请求
- 服务器收到请求，调用对应的servlet进行处理;servlet处理完成会有响应信息生成
- 浏览器收到了服务器响应的数据，把之前的页面清除，展示新的数据(效果就是页面刷新)

现在的交互(XmlHttpRequest对象)

- XMLHttpRequest对象帮我们发送请求
- 服务器收到请求，调用对应的servlet进行处理；servlet处理完成会有相应信息生成
- XMLHttpRequest对象收到数据(浏览器就感受不到这个数据了;xml对象收到这个数据)

```js
var xhr= new XMLHttpRequest0://创建xhr对象;
xhr.open("GET","login",true);//建立连接;
xhr.send0://通过地道传输数据

//监听xhr的状态
xhr.onreadystatechange=function()
{
    if (xmlhttp.readystate= =4 && xmlhttp.status== 200)
    {
        document.getElementByldC" myDiv ").inner
```

![浏览器与服务器交互模式](img\浏览器与服务器交互模式x2.png)

## Jquery对AJAX的操作
- $.get()

示例
```js
$("[#ID]").Cclick(function(){
  //$.get(ur1，[data], [callback], [type])
  //[]代表这个参数可以不用传递
  //data:传递的数据: "k=b&k=v" 传递一个js对象
  //callback: 定义一个回调函数，随便定义一个参数，这个参数就封装了服务器返回的数据
  //type:返回的数据类型;可以不写，自动判断
  //type:返回内容格式，xm1,html,script,json,text,_default. 
  $.get("${ctp}/getinfo",
  {lastName: "长萨",age:18},
  fuction(abc){
    //abc代表服务器给我们的数据，如果服务器转发到一个页面，data代表整个页面;
    //alert(abc);
    $("[id]").append(abc);
  });//支持EL表达式
  return false;
})
```
- $.post()
- $.ajax()

改变了我们传统的交互方式:

1. 发请求
2. 服务器收到请求,处理请求经常要给页面携带数据 regueststtribute("map",map);转发到页面
3. 浏览器收到页面数据.在页面使用el表达式获取数据;
导致页面整个刷新;造成很大的服务器负担;

只让服务器返回我们需要的部分数据即可;不用返回整个页面;xhr替代浏览器来接爱响应,发送请求;利用dom增删改的方式来改变页面效果;

异步无刷新页面技术

- 异步:不会阻塞浏览器
- 同步:会阻塞浏览器，因为需要等到服务器整个处理完请求，完成响应后才能做其他事情


