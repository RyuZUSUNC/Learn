# CVE-2018-11784 (Tomcat URL 跳转漏洞)

## 漏洞存在版本
- 9.0.0.M1 - 9.0.11
- 8.5.0 - 8.5.33
- 7.0.23 - 7.0.90

## 漏洞描述
默认servlet返回到一个目录的重定向（例如，当用户请求'/foo'时重定向到'/foo/’），一个特制的URL可用于导致重定向生成到攻击者选择的任何URI。

## 漏洞测试/确认
构造URL

```
http://[TomcatIP:Port]//[baidu.com]/..;/[可访问目录/可访问目录]
```

默认存在的docs目录也可以被利用，例

```
http://[TomcatIP:Port]//[baidu.com]/..;/docs/images
```

