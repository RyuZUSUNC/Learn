# 手动添加分流规则

点击软件Setting，找到Profiles（配置文件下）的Parsers。点击Edit （整个文档编写符合yaml语法规范）：

```yaml
parsers: # array
  - url: https://xxxxxxx.ini (订阅地址 Profiles中右键选择Setting查看)
    yaml:
      prepend-rules:
        - DOMAIN-SUFFIX,openai.com,🇺🇸 Large 美国01 - allmedia | IEPL | 倍率:1.8
        - DOMAIN-SUFFIX,anthropic.com,🇺🇸 Large 美国01 - allmedia | IEPL | 倍率:1.8
        - DOMAIN-SUFFIX,claude.ai,🇺🇸 Large 美国01 - allmedia | IEPL | 倍率:1.8
```

```js
DOMAIN-SUFFIX：域名后缀匹配
DOMAIN：域名匹配
DOMAIN-KEYWORD：域名关键字匹配
IP-CIDR：IP段匹配
SRC-IP-CIDR：源IP段匹配
GEOIP：GEOIP数据库（国家代码）匹配
DST-PORT：目标端口匹配
SRC-PORT：源端口匹配
PROCESS-NAME：源进程名匹配
RULE-SET：Rule Provider规则匹配
MATCH：全匹配
```