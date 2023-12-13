# Json Web Token(JWT)
JSON Web Token（JWT）是一个非常轻巧的规范。这个规范允许我们使用JWT在两个组织之间传递安全可靠的信息。

JSON Web Token (JWT) is a compact URL-safe means of representing claims to be transferred between two parties

# JSON Web Signature(JWS)

JSON Web Signature是一个有着简单的统一表达形式的字符串

示例：
![](\img\JWS1.webp)

主要分为以下三部分
## 头部（Header）
用于描述关于该JWT的最基本的信息，例如其类型以及签名所用的算法等。这也可以被表示成一个JSON对象。

例如
```json
{
  "typ": "JWT",
  "alg": "HS256"
}
```

## 载荷（PayLoad）
自定义的数据，一般存储用户Id，过期时间等信息。也就是JWT的核心所在，因为这些数据就是使后端知道此token是哪个用户已经登录的凭证。而且这些数据是存在token里面的，由前端携带，所以后端几乎不需要保存任何数据。

JWT指定七个默认字段供选择。

- iss：发行人
- exp：到期时间
- sub：主题
- aud：用户
- nbf：在此之前不可用
- iat：发布时间
- jti：JWT ID用于标识该JWT

除以上默认字段外，我们还可以自定义私有字段

例如
```json
{
  "uid": "xxxxidid",  //用户id
  "exp": "12121212"  //过期时间
}
```

## 签名（signature）
头部和载荷各自base64加密后用.连接起来，然后就形成了xxx.xx的前两段token。

最后一段token的形成是，前两段加入一个密匙用HS256算法或者其他算法加密形成。



# JSON Web Encryption(JWE)