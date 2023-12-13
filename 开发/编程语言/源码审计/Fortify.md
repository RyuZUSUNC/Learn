## 添加扫描参数
Enable translation
```
"-64"
"-Xmx16G"
"-encoding"
"UTF-8"

```

Enable scan
```
"-64"
"-Xmx16G"
"-encoding"
"UTF-8"
    
```


- enable clean :把上一次的扫描结果清楚，除非换一个build ID,不然中间文件可能对下一次扫描产生影响。
- enable translation: 转换，把源码代码转换成nst文件

- -64： 是扫描64位的模式，sca默认扫描是32位模式。
- -Xmx4000m:4000M大概是4G，制定内存数-Xmx4G ：也可以用G定义这个参数建议加
- -encoding: 定制编码，UTF-8比较全，工具解析代码的时候指定字符集转换的比较好，建议加，如果中文注释不加会是乱码。
- -diable-source-:rendering:不加载与漏洞无关的代码到审计平台上，不建议加，这样代码显示不全。


## 审计
将Fortify SCA 扫描分析出来的结果中的漏洞进行审查，分析，定性，指导开发人员进行漏洞的修复工作。

Hide/Suppress/Suspicious/Not An Issue四个的不同
- Hide: 是将此漏洞不显示出来，在报告中也不显示出来
- Suppress:是此漏洞不是问题，可以不用看的
- Suspicious: 是审计的一个定性，这个问题有可能是真的，值得怀疑。
- Not An Issue: 也是审计的一个定性，说明这一漏洞不是个问题。
