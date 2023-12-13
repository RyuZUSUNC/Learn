https://blog.csdn.net/weixin_40022980/article/details/83653386

# 名词释义
- RESTful:URL定位资源，用HTTP动词（GET,POST,PUT,DELETE)描述操作。
   - Resource：资源，即数据。
   - Representational：某种表现形式，比如用JSON，XML，JPEG等；
   - State Transfer：状态变化。通过HTTP动词实现。

所以RESTful API就是REST风格的API。

# 设计目的
Client 和 Server 端进一步 解耦 

# 设计特点
安全可靠，高效，易扩展
简单明了，可读性强，没有歧义
API风格统一，调用规则，传入参数和返回数据有统一的标准

# 设计规则
## HTTPS
https 为接口的安全提供了保障,可以有效防止通信被窃听和篡改, 而且现在部署https的成本越来越低,可以通过 cerbot 等工具, 方便快速的制作免费的安全证书,所以生产环境,务必使用 https.

## 域名
应当尽可能的将API与其主域名区分开,可以使用专用的域名访问API,例如(推荐使用):

```
https://api.ffffffff0x.com 
```

或者可以放到主域名下,例如:

```
https://www.ffffffff0x.com/api 
```

## 版本控制
随着业务的发展,需求的不断变化, API的迭代是必然的,很可能当前版本正在使用, 而我们就得开发甚至上线一个不兼容的版本, 为了让旧用户可以正常使用,为了保证开发的顺利进行,我们需要控制好API的版本.

通常情况下, 有两种做法:

将版本号直接加入URL中

```
https://api.ffffffff0x.com/v1 
https://api.ffffffff0x.com/v2 
```

使用HTTP请求头的Accept字段进行区分

```
 https://api.ffffffff0x.com/
    Accept: application/prs.ffffffff0x.v1+json
    Accept: application/prs.ffffffff0x.v2+json
```

## 用URL定位资源
在 restful 的架构中,所有的一切表示资源,每一个URL都代表这一种资源,资源应当是一个名词, 而且大部分情况下是名词的附属,尽量不要在URL中出现动词

github的例子:

```
GET /issues                                     列出所有的issues
GET /orgs/:org/issues                           列出某个项目的 issues
GET /repos/:owner/:repo/issues/:number          获取某个项目的某个 issue
POST /repos/:owner/:repo/issues                 为某个项目创建 issue
PATCH /repos/:owner/:repo/issues/:number        修改某个issue
PUT /repos/:owner/:repo/issues/:number/lock     锁住某个issue
DELETE /repos/:owner/:repo/issues/:number/lock  接收某个issue
```

例子中冒号开始的代表变量，例如 /repos/summerblue/larabbs/issues

在github的实现中, 我们可以总结出:

资源的设计可以嵌套,表明资源与资源之间的关系。

大部分的情况下我们访问的是某个资源集合,想得到单个资源可以通过资源的id 或 number等唯一标识获取

某些情况下 资源会是单数形式,例如某个项目某个issue的锁,每一个issue只会有一把锁,所以它是单数

错误例子:

```
POST https://api.larabbs.com/createTopic
GET https://api.larabbs.com/topic/show/1
POST https://api.larabbs.com/topics/1/comments/create
POST https://api.larabbs.com/topics/1/comments/100/delete
```

正确的例子：

```
POST https://api.larabbs.com/topics
GET https://api.larabbs.com/topics/1
POST https://api.larabbs.com/topics/1/comments
DELETE https://api.larabbs.com/topics/1/comments/100
```

## 用HTTP动词描述操作
Http设计了很多动词, 来标识不同的操作, RESTful 很好的利用的这一点, 我们需要正确的使用HTTP 动词, 来表明我们如何操作资源.

## 资源过滤
我们需要提供合理的参数供客户端过滤资源, 例如:

```
?state=closed: 不同状态的资源
?page=2&per_page=100：访问第几页数据，每页多少条。
?sortby=name&order=asc：指定返回结果按照哪个属性排序，以及排序顺序。
```

## 正确的使用状态码
HTTP提供了丰富的状态码,正确的使用状态码可以让相应的数据具有可读性。

在状态码的设计编排上尽量遵守HTTP的状态码,

## 数据相应格式
考虑到响应数据的可读性及通用性，默认使用 JSON 作为数据响应格式。如果客户端有需求使用其他的响应格式，例如 XML，需要在 Accept 头中指定需要的格式。

```
https://api.ffffffff0x.com/
    Accept: application/prs.ffffffff0x.v1+json
    Accept: application/prs.ffffffff0x.v1+xml
```

对于错误数据,默认使用个如下结构:

```
'messgae'=>':messgae'   //错误的具体描述
'errors'=>':errors',    // 参数的具体错误描述, 422 等状态提供
'code'=>':code',    // 自定义的异常码,
'status_code'=>':status_code', // http状态码
'debug'=>':debug'  // debug 信息, 非生产环境提供
```

例如:

```json
{
    "message": "422 Unprocessable Entity",
    "errors": {
        "name": [
            "姓名 必须为字符串。"
        ]
    },
    "status_code": 422
}
{
    "message": "您无权访问该订单",
    "status_code": 403
}
```

## 调用的频率限制
为了防止服务器被攻击，减少服务器压力，需要对接口进行合适的限流控制，需要在响应头信息中加入合适的信息，告知客户端当前的限流情况

```
X-RateLimit-Limit :100 最大访问次数
X-RateLimit-Remaining :93 剩余的访问次数
X-RateLimit-Reset :1513784506 到该时间点，访问次数会重置为 X-RateLimit-Limit
```

超过限流次数后，需要返回 429 Too Many Requests 错误。

## 编写文档
为了方便用户使用，我们需要提供清晰的文档，尽可能包括以下几点:

包括每个接口的请求参数，每个参数的类型限制，是否必填，可选的值等。 响应结果的例子说明，包括响应结果中，每个参数的释义。 对于某一类接口，需要有尽量详细的文字说明，比如针对一些特定场景，接口应该如何调用。