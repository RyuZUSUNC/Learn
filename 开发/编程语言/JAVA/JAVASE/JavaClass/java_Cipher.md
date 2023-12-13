javax.crypto.Cipher，翻译为密码，其实叫做密码器更加合适。Cipher是JCA(Java Cryptographic Extension，Java加密扩展)的核心，提供基于多种加解密算法的加解密功能。

http://www.throwable.club/2019/02/16/java-security-cipher/

# Cipher初始化transformation(转换模式)的一些知识补充

转换模式transformation一般由三个部分组成，格式是：算法/工作模式/填充模式(algorithm/mode/padding)。

例如：DES/CBC/PKCS5Padding。

## 算法
算法就是指具体加解密算法的名称英文字符串，例如"SHA-256"、"RSA"等

## 工作模式
工作模式其实主要是针对分组密码。分组密码是将明文消息编码表示后的数字（简称明文数字）序列，划分成长度为n的组（可看成长度为n的矢量），每组分别在密钥的控制下变换成等长的输出数字（简称密文数字）序列。工作模式的出现主要基于下面原因：

- 当需要加密的明文长度十分大(例如文件内容)，由于硬件或者性能原因需要分组加密。
- 多次使用相同的密钥对多个分组加密，会引发许多安全问题。

从本质上讲，工作模式是一项增强密码算法或者使算法适应具体应用的技术，例如将分组密码应用于数据块组成的序列或者数据流。目前主要包括下面五种由NIST定义的工作模式：

  - ECB：Electronic CodeBook mode（电子密码模式）
    - 用相同的密钥分别对明文分组独立加密
      - 单个数据的安全传输(例如一个加密密钥)

  - CBC：Cipher Block Chaining mode（密码分组链接模式）
    - 加密算法的输入是上一个密文组合下一个明文组的异或
      - 面向分组的通用传输或者认证

  - CFB：Cipher FeedBack mode（密文反馈模式）
    - 一次处理s位，上一块密文作为加密算法的输入，产生的伪随机数输出与明文异或作为下一单元的密文
      - 面向分组的通用传输或者认证

  - OFB：Output FeedBack mode（输出反馈模式）
    - 与CFB类似，只是加密算法的输入是上一次加密的输出，并且使用整个分组
      - 噪声信道上的数据流的传输(如卫星通信)

  - CTR：CounTeR mode（计数器模式）
    - 每个明文分组都与一个经过加密的计数器相异或。对每个后续分组计数器递增
      - 面向分组的通用传输或者用于高速需求

上面五种工作模式可以用于3DES和AES在内的任何分组密码

## 填充模式

Padding指的是：块加密算法要求原文数据长度为固定块大小的整数倍，如果原文数据长度大于固定块大小，则需要在固定块填充数据直到整个块的数据是完整的。例如我们约定块的长度为128，但是需要加密的原文长度为129，那么需要分成两个加密块，第二个加密块需要填充127长度的数据，填充模式决定怎么填充数据。

对数据在加密时进行填充、解密时去除填充则是通信双方需要重点考虑的因素。对原文进行填充，主要基于以下原因：

- 首先，考虑安全性。由于对原始数据进行了填充，使原文能够“伪装”在填充后的数据中，使得攻击者很难找到真正的原文位置。
- 其次，由于块加密算法要求原文数据长度为固定块大小的整数倍，如果加密原文不满足这个条件，则需要在加密前填充原文数据至固定块大小的整数倍。
- 另外，填充也为发送方与接收方提供了一种标准的形式以约束加密原文的大小。只有加解密双方知道填充方式，才可知道如何准确移去填充的数据并进行解密。

常用的填充方式至少有5种，不同编程语言实现加解密时用到的填充多数来自于这些方式或它们的变种方式。以下五种填充模式摘抄自参考资料的论文：

1. 填充数据为填充字节序列的长度：

这种填充方式中，填充字符串由一个字节序列组成，每个字节填充该字节序列的长度。假定块长度为8，原文数据长度为9，则填充字节数 等于0x07；如果明文数据长度为8的整数倍，则填充字节数为0x08。填充字符串如下：

```
原文数据1: FF FF FF FF FF FF FF FF FF
填充后数据1:FF FF FF FF FF FF FF FF FF 07 07 07 07 07 07 07
==========================================================
原文数据2:FF FF FF FF FF FF FF FF
填充后数据2:FF FF FF FF FF FF FF FF 08 08 08 08 08 08 08 08
```

2. 填充数据为0x80后加0x00：

这种填充方式中，填充字符串的第一个字节数是0x80，后面的每个字节是0x00。假定块长度为8，原文数据长度为9或者为8的整数倍，则 填充字符串如下：

```
原文数据1: FF FF FF FF FF FF FF FF FF
填充后数据1:FF FF FF FF FF FF FF FF FF 80 00 00 00 00 00 00
==========================================================
原文数据2:FF FF FF FF FF FF FF FF
填充后数据2:FF FF FF FF FF FF FF FF 80 00 00 00 00 00 00 00
```

3. 填充数据的最后一个字节为填充字节序列的长度：

这种填充方式中，填充字符串的最后一个字节为该序列的长度，而前面的字节可以是0x00，也可以是随机的字节序列。假定块长度为8，原文数据长度为9或者为8的整数倍，则填充字符串如下：

```
原文数据1:FF FF FF FF FF FF FF FF FF
填充后数据1:FF FF FF FF FF FF FF FF FF 00 00 00 00 00 00 07或FF FF FF FF FF FF FF FF FF 0A B0 0C 08 05 09 07
===============================================================================
原文数据2:FF FF FF FF FF FF FF FF
填充后数据2:FF FF FF FF FF FF FF FF 00 00 00 00 00 00 00 08或FF FF FF FF FF FF FF FF 80 06 AB EA 03 02 01 08
```

4. 填充数据为空格：

这种填充方式中，填充字符串的每个字节为空格对应的字节数0x20。假定块长度为8，原文数据长度为9或者为8的整数倍，则填充字符串如下：

```
原文数据1: FF FF FF FF FF FF FF FF FF
填充后数据1:FF FF FF FF FF FF FF FF FF 20 20 20 20 20 20 20
===============================================================================
原文数据2:FF FF FF FF FF FF FF FF
填充后数据2:FF FF FF FF FF FF FF FF 20 20 20 20 20 20 20 20
```

5. 填充数据为0x00：

这种填充方式中，填充字符串的每个字节为0x00。假定块长度为8，原文数据长度为9或者8的整数倍，则填充字符串如下：

```
原文数据1: FF FF FF FF FF FF FF FF FF
填充后数据1:FF FF FF FF FF FF FF FF FF 00 00 00 00 00 00 00
===============================================================================
原文数据2:FF FF FF FF FF FF FF FF
填充后数据2:FF FF FF FF FF FF FF FF 00 00 00 00 00 00 00 00
```

# transformation小结
SunJCE Provider支持的Cipher的部分详细信息如下：

![Cipher支持的算法列表](..\img\Cipher支持的算法列表.png)

Java原生支持的Padding(Cipher)汇总如下：

![Java原生支持的Padding方法](..\img\Java原生支持的Padding方法.png)

其他Padding需要第三方Provider提供。

# Cipher的属性和方法
## Cipher的七个主要公有属性
1. ENCRYPT_MODE，整型值1，加密模式，用于Cipher的初始化。
2. DECRYPT_MODE，整型值2，解密模式，用于Cipher的初始化。
3. WRAP_MODE，整型值3，包装密钥模式，用于Cipher的初始化。
4. UNWRAP_MODE，整型值4，解包装密钥模式，用于Cipher的初始化。
5. PUBLIC_KEY，整型值1，解包装密钥模式下指定密钥类型为公钥。
6. PRIVATE_KEY，整型值2，解包装密钥模式下指定密钥类型为私钥。
7. SECRET_KEY，整型值3，解包装密钥模式下指定密钥类型为密钥，主要用于不是非对称加密的密钥(只有一个密钥，不包含私钥和公钥)。

## getInstance方法

Cipher提供三个静态工厂方法getInstance()用于构建其实例，三个方法如下：

```java
public static final Cipher getInstance(String transformation)
                                throws NoSuchAlgorithmException,
                                       NoSuchPaddingException

public static final Cipher getInstance(String transformation,
                                       String provider)
                                throws NoSuchAlgorithmException,
                                       NoSuchProviderException,
                                       NoSuchPaddingException

public static final Cipher getInstance(String transformation,
                                       Provider provider)
                                throws NoSuchAlgorithmException,
                                       NoSuchPaddingException
```

其中 transformation，这里称为`转换(模式)`，是核心参数，见前面一个小节的解析。另外，有两个工厂方法要求必须传入 java.security.Provider 的全类名或者实例，因为 Cipher 要从对应的提供商中获取指定转换模式的实现，第一个工厂方法只有单参数transformation，它会从现成所有的`java.security.Provider`中匹配取出第一个满足transformation的服务，从中实例化`CipherSpi `(`要理解Cipher委托到内部持有的CipherSpi实例完成具体的加解密功能`)。实际上Cipher 实例的初始化必须依赖于转换模式和提供商。

## init方法

init()方法一共有八个变体方法，此方法主要用于初始化Cipher。

```java
//额外参数是Key(密钥)
public final void init(int opmode,
                       Key key)
                throws InvalidKeyException

//额外参数是Key(密钥)和SecureRandom(随机源)
public final void init(int opmode,
                       Key key,
                       SecureRandom random)
                throws InvalidKeyException

//额外参数是Key(密钥)和AlgorithmParameterSpec(算法参数透明定义)
public final void init(int opmode,
                       Key key,
                       AlgorithmParameterSpec params)
                throws InvalidKeyException,
                       InvalidAlgorithmParameterException 

//额外参数是Key(密钥)、AlgorithmParameterSpec(算法参数透明定义)和SecureRandom(随机源)
public final void init(int opmode,
                       Key key,
                       AlgorithmParameterSpec params,
                       SecureRandom random)
                throws InvalidKeyException,
                       InvalidAlgorithmParameterException

//额外参数是Key(密钥)、AlgorithmParameters(算法参数)
public final void init(int opmode,
                       Key key,
                       AlgorithmParameters params)
                throws InvalidKeyException,
                       InvalidAlgorithmParameterException

//额外参数是Key(密钥)、AlgorithmParameters(算法参数)、SecureRandom(随机源)
public final void init(int opmode,
                       Key key,
                       AlgorithmParameters params,
                       SecureRandom random)
                    throws InvalidKeyException,
                       InvalidAlgorithmParameterException

//额外参数是Certificate(证书)
public final void init(int opmode,
                       Certificate certificate)
                throws InvalidKeyException

//额外参数是Certificate(证书)、SecureRandom(随机源)
public final void init(int opmode,
                       Certificate certificate,
                       SecureRandom random)
                throws InvalidKeyException
```

opmode(操作模式) 是必须参数，可选值是`ENCRYPT_MODE`、`DECRYPT_MODE`、`WRAP_MODE`和`UNWRAP_MODE`。Key 类型参数如果不是非对称加密，对应的类型是 SecretKey ，如果是非对称加密，可以是 PublicKey 或者 PrivateKey。SecureRandom 是随机源，因为有些算法需要每次加密结果都不相同，这个时候需要依赖系统或者传入的随机源，一些要求每次加解密结果相同的算法如 AES 不能使用此参数。Certificate 是带有密钥的证书实现。算法参数主要包括 IV(initialization vector，初始化向量) 等等。

## wrap方法和unwrap方法

wrap方法用于包装一个密钥。

···java
public final byte[] wrap(Key key)
                  throws IllegalBlockSizeException,
                         InvalidKeyException
···

wrap方法使用的时候需要注意Cipher的opmode要初始化为`WRAP_MODE`。

unwrap方法用于解包装一个密钥。

```java
public final Key unwrap(byte[] wrappedKey,
                        String wrappedKeyAlgorithm,
                        int wrappedKeyType)
                 throws InvalidKeyException,
                        NoSuchAlgorithmException
```

unwrap方法使用的时候需要注意Cipher的opmode要初始化为`UNWRAP_MODE`，在调用unwrap方法时候，需要指定之前包装密钥的算法和Key的类型。

其实wrap和unwrap是一个互逆的操作：

- wrap方法的作用是把原始的密钥通过某种加密算法包装为加密后的密钥，这样就可以避免在传递密钥的时候泄漏了密钥的明文。
- unwrap方法的作用是把包装(加密)后的密钥解包装为原始的密钥，得到密钥的明文。

```java
public enum EncryptUtils {

    /**
     * 单例
     */
    SINGLETON;

    private static final String SECRECT = "passwrod";

    public String wrap(String keyString) throws Exception {
        KeyGenerator keyGenerator = KeyGenerator.getInstance("AES");
        //初始化密钥生成器，指定密钥长度为128，指定随机源的种子为指定的密钥(这里是"passward")
        keyGenerator.init(128, new SecureRandom(SECRECT.getBytes()));
        SecretKey secretKey = keyGenerator.generateKey();
        SecretKeySpec secretKeySpec = new SecretKeySpec(secretKey.getEncoded(), "AES");
        Cipher cipher = Cipher.getInstance("AES");
        cipher.init(Cipher.WRAP_MODE, secretKeySpec);
        SecretKeySpec key = new SecretKeySpec(keyString.getBytes(), "AES");
        byte[] bytes = cipher.wrap(key);
        return Hex.encodeHexString(bytes);
    }

    public String unwrap(String keyString) throws Exception {
        byte[] rawKey = Hex.decodeHex(keyString);
        KeyGenerator keyGenerator = KeyGenerator.getInstance("AES");
        //初始化密钥生成器，指定密钥长度为128，指定随机源的种子为指定的密钥(这里是"passward")
        keyGenerator.init(128, new SecureRandom(SECRECT.getBytes()));
        SecretKey secretKey = keyGenerator.generateKey();
        SecretKeySpec secretKeySpec = new SecretKeySpec(secretKey.getEncoded(), "AES");
        Cipher cipher = Cipher.getInstance("AES");
        cipher.init(Cipher.UNWRAP_MODE, secretKeySpec);
        SecretKey key = (SecretKey) cipher.unwrap(rawKey, "AES", Cipher.SECRET_KEY);
        return new String(key.getEncoded());
    }

    public static void main(String[] args) throws Exception {
        String wrapKey = EncryptUtils.SINGLETON.wrap("doge");
        System.out.println(wrapKey);
        System.out.println(EncryptUtils.SINGLETON.unwrap(wrapKey));
    }
}
```

上面的例子是通过AES对密钥进行包装和解包装，调用main方法，输出：

```
77050742188d4b97a1d401db902b864d
doge
```

## update方法

update方法有多个变体，其实意义相差无几：

```java
public final byte[] update(byte[] input)

public final byte[] update(byte[] input,
                           int inputOffset,
                           int inputLen)

public final int update(byte[] input,
                        int inputOffset,
                        int inputLen,
                        byte[] output)
                 throws ShortBufferException

public final int update(ByteBuffer input,
                        ByteBuffer output)
                 throws ShortBufferException
```

update方法主要用于部分加密或者部分解密，至于加密或是解密取决于Cipher初始化时候的opmode。

即使它有多个变体，但是套路是一样的：依赖于一个输入的缓冲区(带有需要被加密或者被解密的数据)、返回值或者参数是一个输出的缓冲区，一些额外的参数可以通过偏移量和长度控制加密或者解密操作的数据段。

部分加密或者解密操作完毕后，必须要调用`Cipher#doFinal()`方法来结束加密或者解密操作。

## doFinal方法

`doFinal()`方法也存在多个变体：

```java
/**
 * 结束多部分加密或者解密操作。
 * 此方法需要在update调用链执行完毕之后调用，返回的结果是加密或者解密结果的一部分。
 * 此方法正常调用结束之后Cipher会重置为初始化状态。
 */
public final byte[] doFinal()
                     throws IllegalBlockSizeException,
                            BadPaddingException

/**
 * 结束多部分加密或者解密操作。
 * 此方法需要在update调用链执行完毕之后调用，传入的output作为缓冲区接收加密或者解密结果的一部分。
 * 此方法正常调用结束之后Cipher会重置为初始化状态。
 */
public final int doFinal(byte[] output,
                         int outputOffset)
                  throws IllegalBlockSizeException,
                         ShortBufferException,
                         BadPaddingException                         

/**
 * 结束单部分加密或者解密操作。
 * 此方法接收需要加密或者解密的完整报文，返回处理结果
 * 此方法正常调用结束之后Cipher会重置为初始化状态。
 */
public final byte[] doFinal(byte[] input)
                     throws IllegalBlockSizeException,
                            BadPaddingException

/**
 * 结束单部分或者多部分加密或者解密操作。
 * 参数inputOffset为需要加解密的报文byte数组的起始位置，inputLen为需要加密或者解密的字节长度
 * 此方法正常调用结束之后Cipher会重置为初始化状态。
 */
public final byte[] doFinal(byte[] input,
                            int inputOffset,
                            int inputLen)
                     throws IllegalBlockSizeException,
                            BadPaddingException      

/**
 * 结束单部分或者多部分加密或者解密操作。
 * 参数inputOffset为需要加解密的报文byte数组的起始位置，inputLen为需要加密或者解密的字节长度，output用于接收加解密的结果
 * 此方法正常调用结束之后Cipher会重置为初始化状态。
 */
public final int doFinal(byte[] input,
                         int inputOffset,
                         int inputLen,
                         byte[] output)
                  throws ShortBufferException,
                         IllegalBlockSizeException,
                         BadPaddingException                                                         

/**
 * 结束单部分或者多部分加密或者解密操作。
 * 参数inputOffset为需要加解密的报文byte数组的起始位置，inputLen为需要加密或者解密的字节长度，
 * output用于接收加解密的结果，outputOffset用于设置output的起始位置
 * 此方法正常调用结束之后Cipher会重置为初始化状态。
 */
public final int doFinal(byte[] input,
                         int inputOffset,
                         int inputLen,
                         byte[] output,
                         int outputOffset)
                  throws ShortBufferException,
                         IllegalBlockSizeException,
                         BadPaddingException 
/**
 * 结束单部分或者多部分加密或者解密操作。
 * 参数input为输入缓冲区，output为输出缓冲区
 * 此方法正常调用结束之后Cipher会重置为初始化状态。
 */
public final int doFinal(ByteBuffer input,
                         ByteBuffer output)
                  throws ShortBufferException,
                         IllegalBlockSizeException,
                         BadPaddingException                  
```

doFinal()主要功能是结束单部分或者多部分加密或者解密操作。

单部分加密或者解密适用于需要处理的报文长度较短无需分块的情况，这个时候直接使用byte[] doFinal(byte[] input)方法即可。

多部分加密或者解密适用于需要处理的报文长度长度较大，需要进行分块的情况，这个时候需要调用多次update方法变体进行部分块的加解密，最后调用doFinal方法变体进行部分加解密操作的结束。

举个例子，例如处理块的大小为8，实际需要加密的报文长度为23，那么需要分三块进行加密，前面2块长度为8的报文需要调用update进行部分加密，部分加密的结果可以从update的返回值获取到，最后的7长度(其实一般会填充到长度为块长度8)的报文则调用doFinal进行加密，结束整个部分加密的操作。

另外，值得注意的是只要Cipher正常调用完任一个doFinal变体方法(过程中不抛出异常)，那么Cipher会重置为初始化状态，可以继续使用，这个可复用的特性可以降低创建Cipher实例的性能损耗。

## updateADD方法

首先ADD的意思是Additional Authentication Data(额外的身份认证数据)。updateADD()也有三个方法变体：

```java
public final void updateAAD(byte[] src)

public final void updateAAD(byte[] src,
                            int offset,
                            int len)

public final void updateAAD(ByteBuffer src)
```

它的方法变体都只依赖一个输入缓冲区，带有额外的身份认证数据，一般使用在`GCM`或者`CCM`加解密算法中。如果使用此方法，它的调用必须在Cipher的update和doFinal变体方法之前调用，其实理解起来也很简单，身份验证必须在实际的加解密操作之前进行。目前，updateADD的资料比较少，笔者在生产环境找那个也尚未实践过，所以不做展开分析。

## 其他方法
其他方法主要是Getter方法，用于获取Cipher的相关信息。

- `public final Provider getProvider()`：获取Cipher的提供商。
- `public final String getAlgorithm()`：获取Cipher使用的算法名称。
- `public final int getBlockSize()`：分组加密中，每一组都有固定的长度，也称为块，此方法是返回块的大小（以字节为单位）。
- `public final int getOutputSize(int inputLen)`：根据给定的输入长度inputLen（以字节为单位），返回保存下一个update或doFinal操作结果所需的输出缓冲区长度（以字节为单位）。
- `public final byte[] getIV()`：返回Cipher中的初始化向量的字节数组。
- `public final AlgorithmParameters getParameters()`：返回Cipher使用的算法参数。
- `public final ExemptionMechanism getExemptionMechanism()`：返回Cipher使用的豁免(exemption)机制对象。
- `public static final int getMaxAllowedKeyLength(String transformation)`：根据所安装的JCE策略文件，返回指定转换的最大密钥长度。
- `public static final AlgorithmParameterSpec getMaxAllowedParameterSpec(String transformation)`：根据JCE策略文件，返回Cipher指定transformation下最大的AlgorithmParameterSpec对象。

# Cipher 工作流程

主要过程包括：

1. 创建Cipher实例，这个时候会从平台中所有的提供商(Provider)中根据transformation匹配第一个可以使用的CipherSpi实例，"算法/工作模式/填充模式"必须完全匹配才能选中。
```
在${JAVA_HONE}/jre/lib/security中的java.security文件中可以看到默认加载的提供商。
如果需要添加额外或者自实现的Provider，可以通过java.security.Security的静态方法addProvider添加。
```

2. 通过Cipher实例的init方法初始化Cipher，主要参数是opmode和密钥。
3. 根据初始化的方式和是否需要分组处理，选择合适的方法进行调用，一般以doFinal()方法作结得到返回结果。

# Cipher的使用

为了方便Cipher的使用，最好先引入apache-codec依赖，这样能简化Hex、Base64等操作。

```xml
<dependency>
    <groupId>commons-codec</groupId>
    <artifactId>commons-codec</artifactId>
    <version>1.10</version>
</dependency>
```

大多数情况下，加密后的byte数组的中元素取值不在Unicode码点的范围内，表面上看到的就是乱码，实际上它们是有意义的，因此需要考虑把这种byte数组转换为非乱码的字符串以便传输，常见的方式有Hex(二进制转换为十六进制)、Base64等等。

下面举例中没有针对异常类型进行处理统一外抛，切勿模仿，还有，所有的字符串转化为字节数组都没有指定字符编码，因此只能使用非中文的明文进行处理。

## 加密模式

加密模式下，Cipher只能用于加密，主要由`init()`方法中的opmode决定。

举个例子：
```java
public String encryptByAes(String content, String password) throws Exception {
	//这里指定了算法为AES_128，工作模式为ECB，填充模式为NoPadding
	Cipher cipher = Cipher.getInstance("AES_128/ECB/NoPadding");
	KeyGenerator keyGenerator = KeyGenerator.getInstance("AES");
	//因为AES要求密钥的长度为128，我们需要固定的密码，因此随机源的种子需要设置为我们的密码数组
	keyGenerator.init(128, new SecureRandom(password.getBytes()));
	SecretKey secretKey = keyGenerator.generateKey();
	SecretKeySpec secretKeySpec = new SecretKeySpec(secretKey.getEncoded(), "AES");
	//基于加密模式和密钥初始化Cipher
	cipher.init(Cipher.ENCRYPT_MODE, secretKeySpec);
	//单部分加密结束，重置Cipher
	byte[] bytes = cipher.doFinal(content.getBytes());
	//加密后的密文由二进制序列转化为十六进制序列，依赖apache-codec包
	return Hex.encodeHexString(bytes);
}
```

其实整个过程Cipher的使用都很简单，比较复杂的反而是密钥生成的过程。上面的例子需要注意，因为使用了填充模式为NoPadding，输入的需要加密的报文长度必须是16(128bit)的倍数。

## 解密模式

解密模式的使用大致和加密模式是相同的，把处理过程逆转过来就行：

```java
public String decryptByAes(String content, String password) throws Exception {
	//这里要把十六进制的序列转化回二进制的序列，依赖apache-codec包
	byte[] bytes = Hex.decodeHex(content);
	//这里指定了算法为AES_128，工作模式为EBC，填充模式为NoPadding
	Cipher cipher = Cipher.getInstance("AES_128/ECB/NoPadding");
	KeyGenerator keyGenerator = KeyGenerator.getInstance("AES");
	//因为AES要求密钥的长度为128，我们需要固定的密码，因此随机源的种子需要设置为我们的密码数组
	keyGenerator.init(128, new SecureRandom(password.getBytes()));
	SecretKey secretKey = keyGenerator.generateKey();
	SecretKeySpec secretKeySpec = new SecretKeySpec(secretKey.getEncoded(), "AES");
	//基于解密模式和密钥初始化Cipher
	cipher.init(Cipher.DECRYPT_MODE, secretKeySpec);
	//单部分加密结束，重置Cipher
	byte[] result = cipher.doFinal(bytes);
	return new String(result);
}
```

上面的例子需要注意，因为使用了填充模式为NoPadding，输入的需要加密的报文长度必须是16(128bit)的倍数。

## 包装密钥模式和解包装密钥模式

密钥的包装和解包装模式是一对互逆的操作，主要作用是通过算法对密钥进行加解密，从而提高密钥泄漏的难度。

```java
public enum EncryptUtils {

    /**
     * 单例
     */
    SINGLETON;

    private static final String SECRECT = "passwrod";

    public String wrap(String keyString) throws Exception {
        KeyGenerator keyGenerator = KeyGenerator.getInstance("AES");
        //初始化密钥生成器，指定密钥长度为128，指定随机源的种子为指定的密钥(这里是"passward")
        keyGenerator.init(128, new SecureRandom(SECRECT.getBytes()));
        SecretKey secretKey = keyGenerator.generateKey();
        SecretKeySpec secretKeySpec = new SecretKeySpec(secretKey.getEncoded(), "AES");
        Cipher cipher = Cipher.getInstance("AES");
        cipher.init(Cipher.WRAP_MODE, secretKeySpec);
        SecretKeySpec key = new SecretKeySpec(keyString.getBytes(), "AES");
        byte[] bytes = cipher.wrap(key);
        return Hex.encodeHexString(bytes);
    }

    public String unwrap(String keyString) throws Exception {
        byte[] rawKey = Hex.decodeHex(keyString);
        KeyGenerator keyGenerator = KeyGenerator.getInstance("AES");
        //初始化密钥生成器，指定密钥长度为128，指定随机源的种子为指定的密钥(这里是"passward")
        keyGenerator.init(128, new SecureRandom(SECRECT.getBytes()));
        SecretKey secretKey = keyGenerator.generateKey();
        SecretKeySpec secretKeySpec = new SecretKeySpec(secretKey.getEncoded(), "AES");
        Cipher cipher = Cipher.getInstance("AES");
        cipher.init(Cipher.UNWRAP_MODE, secretKeySpec);
        SecretKey key = (SecretKey) cipher.unwrap(rawKey, "AES", Cipher.SECRET_KEY);
        return new String(key.getEncoded());
    }

    public static void main(String[] args) throws Exception {
        String wrapKey = EncryptUtils.SINGLETON.wrap("doge");
        System.out.println(wrapKey);
        System.out.println(EncryptUtils.SINGLETON.unwrap(wrapKey));
    }
}
```

## 分组(部分)加密和分组解密

当一个需要加密的报文十分长的时候，我们可以考虑把报文切割成多个小段，然后针对每个小段进行加密，这就是分组加密。分组解密的过程类同，可以看作是分组加密的逆向过程。

下面还是用AES算法为例举个例子：
```java
import org.apache.commons.codec.binary.Hex;

import javax.crypto.Cipher;
import javax.crypto.KeyGenerator;
import javax.crypto.SecretKey;
import javax.crypto.spec.SecretKeySpec;
import java.security.SecureRandom;

/**
 * @author throwable
 * @version v1.0
 * @description
 * @since 2018/8/15 1:06
 */
public enum Part {

	/**
	 * SINGLETON
	 */
	SINGLETON;

	private static final String PASSWORD = "throwable";

	private Cipher createCipher() throws Exception {
		return Cipher.getInstance("AES");
	}

	public String encrypt(String content) throws Exception {
		Cipher cipher = createCipher();
		KeyGenerator keyGenerator = KeyGenerator.getInstance("AES");
		//因为AES要求密钥的长度为128，我们需要固定的密码，因此随机源的种子需要设置为我们的密码数组
		keyGenerator.init(128, new SecureRandom(PASSWORD.getBytes()));
		SecretKey secretKey = keyGenerator.generateKey();
		SecretKeySpec secretKeySpec = new SecretKeySpec(secretKey.getEncoded(), "AES");
		//基于加密模式和密钥初始化Cipher
		cipher.init(Cipher.ENCRYPT_MODE, secretKeySpec);
		byte[] raw = content.getBytes();
		StringBuilder builder = new StringBuilder();
		//[0,9]
		byte[] first = cipher.update(raw, 0, 10);
		builder.append(Hex.encodeHexString(first));
		//[10,19]
		byte[] second = cipher.update(raw, 10, 10);
		builder.append(Hex.encodeHexString(second));
		//[20,25]
		byte[] third = cipher.update(raw, 20, 6);
		builder.append(Hex.encodeHexString(third));
		//多部分加密结束，得到最后一段加密的结果，重置Cipher
		byte[] bytes = cipher.doFinal();
		String last = Hex.encodeHexString(bytes);
		builder.append(last);
		return builder.toString();
	}

	public String decrypt(String content) throws Exception {
		byte[] raw = Hex.decodeHex(content);
		Cipher cipher = createCipher();
		KeyGenerator keyGenerator = KeyGenerator.getInstance("AES");
		//因为AES要求密钥的长度为128，我们需要固定的密码，因此随机源的种子需要设置为我们的密码数组
		keyGenerator.init(128, new SecureRandom(PASSWORD.getBytes()));
		SecretKey secretKey = keyGenerator.generateKey();
		SecretKeySpec secretKeySpec = new SecretKeySpec(secretKey.getEncoded(), "AES");
		//基于解密模式和密钥初始化Cipher
		cipher.init(Cipher.DECRYPT_MODE, secretKeySpec);
		StringBuilder builder = new StringBuilder();
		//[0,14]
		byte[] first = cipher.update(raw, 0, 15);
		builder.append(new String(first));
		//[15,29]
		byte[] second = cipher.update(raw, 15, 15);
		builder.append(new String(second));
		//[30,31]
		byte[] third = cipher.update(raw, 30, 2);
		builder.append(new String(third));
		//多部分解密结束，得到最后一段解密的结果，重置Cipher
		byte[] bytes = cipher.doFinal();
		builder.append(new String(bytes));
		return builder.toString();
	}

	public static void main(String[] args) throws Exception{
		String raw = "abcdefghijklmnopqrstyuwxyz";
		String e = Part.SINGLETON.encrypt(raw);
		System.out.println(e);
		System.out.println(Part.SINGLETON.decrypt(e));
	}
}
```

上面的分段下标已经在注释中给出，分段的规则由实际情况考虑，一般AES加解密报文不大的时候可以直接单部分加解密即可，这里仅仅是为了做展示。

## 查看当前JDK中Cipher的所有提供商

我们可以直接查看当前的使用的JDK中Cipher的所有提供商和支持的加解密服务，简单写个main函数就行：

```java
import java.security.Provider;
import java.security.Security;
import java.util.Set;

public class Main {

	public static void main(String[] args) throws Exception {
		Provider[] providers = Security.getProviders();
		if (null != providers) {
			for (Provider provider : providers) {
				Set<Provider.Service> services = provider.getServices();
				for (Provider.Service service : services) {
					if ("Cipher".equals(service.getType())) {
						System.out.println(String.format("provider:%s,type:%s,algorithm:%s", service.getProvider(), service.getType(), service.getAlgorithm()));
					}
				}
			}
		}
	}
}
```

## 扩展

因为Java原生支持的transformation是有限的，有些时候我们需要使用一些算法其他工作模式或者填充模式原生无法支持，这个时候我们需要引入第三方的Provider甚至自己实现Provider。常见的第三方Provider是bouncycastle(BC)：

```xml
<dependency>
    <groupId>org.bouncycastle</groupId>
    <artifactId>bcprov-jdk15on</artifactId>
    <version>1.60</version>
</dependency>
```

举个例子，Java原生是不支持AESWRAP算法的，因此可以引入BC的依赖，再使用转换模式AESWRAP。

```java
import org.apache.commons.codec.binary.Hex;
import org.bouncycastle.jce.provider.BouncyCastleProvider;

import javax.crypto.Cipher;
import javax.crypto.KeyGenerator;
import javax.crypto.SecretKey;
import javax.crypto.spec.SecretKeySpec;
import java.security.MessageDigest;
import java.security.SecureRandom;
import java.security.Security;

public enum EncryptUtils {

	/**
	 * SINGLETON
	 */
	SINGLETON;

	private static final String SECRET = "throwable";
	private static final String CHARSET = "UTF-8";

    //装载BC提供商
	static {
		Security.addProvider(new BouncyCastleProvider());
	}


	private Cipher createAesCipher() throws Exception {
		return Cipher.getInstance("AESWRAP");
	}

	public String encryptByAes(String raw) throws Exception {
		Cipher aesCipher = createAesCipher();
		KeyGenerator keyGenerator = KeyGenerator.getInstance("AESWRAP");
		keyGenerator.init(128, new SecureRandom(SECRET.getBytes(CHARSET)));
		SecretKey secretKey = keyGenerator.generateKey();
		SecretKeySpec secretKeySpec = new SecretKeySpec(secretKey.getEncoded(), "AESWRAP");
		aesCipher.init(Cipher.ENCRYPT_MODE, secretKeySpec);
		byte[] bytes = aesCipher.doFinal(raw.getBytes(CHARSET));
		return Hex.encodeHexString(bytes);
	}

	public String decryptByAes(String raw) throws Exception {
		byte[] bytes = Hex.decodeHex(raw);
		Cipher aesCipher = createAesCipher();
		KeyGenerator keyGenerator = KeyGenerator.getInstance("AESWRAP");
		keyGenerator.init(128, new SecureRandom(SECRET.getBytes(CHARSET)));
		SecretKey secretKey = keyGenerator.generateKey();
		SecretKeySpec secretKeySpec = new SecretKeySpec(secretKey.getEncoded(), "AESWRAP");
		aesCipher.init(Cipher.DECRYPT_MODE, secretKeySpec);
		return new String(aesCipher.doFinal(bytes), CHARSET);
	}

	public static void main(String[] args) throws Exception {
		String raw = "throwable-a-doge";
		String en = EncryptUtils.SINGLETON.encryptByAes(raw);
		System.out.println(en);
		String de = EncryptUtils.SINGLETON.decryptByAes(en);
		System.out.println(de);
	}
}
```

# 小结
熟练掌握Cipher的用法、转换模式transformation的一些知识之后，影响我们编写加解密模块代码的主要因素就是加解密算法的原理或者使用，这些需要我们去学习专门的加解密算法相关的知识。

另外，有些时候我们发现不同平台或者不同语言使用同一个加密算法不能相互解密加密，其实原因很简单，绝大部分原因是工作模式选取或者填充模式选取的不同导致的，排除掉这两点，剩下的可能性就是算法的实现不相同，依据这三点因素(或者说就是transformation这唯一的因素)去判断和寻找解决方案即可。