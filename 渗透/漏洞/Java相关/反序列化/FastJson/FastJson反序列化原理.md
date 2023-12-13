>会涉及到Java SPI,ASM

# JNDI 
Java Naming and Directory Interface(Java命令和目录接口)，其提供了很多的实现方式，如RMI,LDAP，CORBA等。

JNDI提供了一个统一的外部接口，底层SPI则是多样的。在使用JNDIReferences的时候可以远程加载外部的对象，即实现factory的初始化。如果说其lookup方法的参数是我们可以控制的，可以将其参数指向我们控制的RMI服务，切换到我们控制的RMI/LDAP服务等等。

攻击流程是这样的，攻击者准备rmi服务和web服务，将rmi绝对路径注入到lookup方法中，受害者JNDI接口会指向攻击者控制rmi服务器，JNDI接口向攻击者控制web服务器远程加载恶意代码，执行构造函数形成RCE。

# 传入JSON字符串(POC)的处理过程
1. `DefaultJSONParser`的初始化
2. 这一步是`parseObject()`是否指定了第二个参数，也就是是否指定了`clazz`字段：

    1. 如果指定了`clazz`字段，则首先根据`clazz`类型来获取相应`deserializer`，如果不是`initDeserializers`中的类的话，则会调用`JavaBeanDeserializer#deserialze`转交`FastjsonASMDeserializer`利用`Fastjson`自己实现的`ASM流程`生成处理类，调用相应的类并将处理流程转交到相应的处理类处理json字符串内容。（这里的描述有一些些问题，后面会尽量相近的描述一下）

    2. 如果未指定，则直接交给`StringCodec`类来处理json字符串。

3. 最终都转交由`DefaultJSONParser#parse`中根据`lexer.token`来选择处理方式，这里的例子中都为`12`也就是`{`(因为要处理json字符串需要一个起始标志位，所以判断当前json字符串的token是很重要的)，接下来就是对json字符串进行处理(这里是一个循环处理，摘取类似"name":"123"这样的关系)。

4. 判断解析的json字符串中是否存在`symbolTable`中的字段（如`@type`，`$ref`这样的字段），如果出现了`@type`则交由`public final Object parseObject(final Map object, Object fieldName)`来处理，然后重复步骤2的过程直到执行成功或报错。

## DefaultJSONParser的初始化过程
由两部分组成

1. `ParserConfig`的初始化
2. `DefaultJSONParser`的初始化

`ParserConfig`的初始化是在`com.alibaba.fastjson.JSON`中调用的

`ParserConfig#ParserConfig`方法中，指定了asm的工厂类，并进行了实例化，一同进行的还有初始化`deserializers`，将用户自定义黑白名单加入到原有的黑白名单中。

`DefaultJSONParser`的初始化是在`com.alibaba.fastjson.JSON#parseObject`中调用并完成的

在初始化了`DefaultJSONParser`之后调用了其`parseObject`方法进行后续的操作

跟进`DefaultJSONParser`可以看到`JSONScanner`的实例化以及`lexer.token`的初始化设置

## 获取对应的derializer
根据上一部分我们可以看到完成初始化操作后主要的处理流程集中于`T value = (T) parser.parseObject(clazz, null);`跟进看一下具体流程。

简单来说就是一个根据`type`获取对应的`derializer`并且调用`derializer.deserialze`进行处理的过程，这里的config是之前初始化的`ParserConfig`。要注意的是`type`这个参数，跟踪整个流程后会发现，如果在写代码时指定了第二个参数如`Group group = JSON.parseObject(jsonString, Group.class);`则第二个参数也就是`Group.class`即为`type`如果未指定第二个参数的话将会获取第一个参数的类型作为`type`，当未指定第二个参数的时候将会调用与第一个参数类型相符的方法来处理。

可以跟进看一下`getDeserializer`的实现

首先会尝试在`deserializers`中匹配`type`的类型，如果匹配到了就返回匹配的`derializer`，否则就判断是否是Class泛型的接口，如果是则调用`getDeserializer((Class<?>) type, type)`继续处理。

当不显示匹配上面的情况时，就会调用`createJavaBeanDeserializer`来创建一个新的`derializer`，并将其加入到`deserializers`这个map中。接下来跟进`createJavaBeanDeserializer`的处理流程。

首先会根据类名和propertyNamingStrategy生成beanInfo，之后利用asm工厂类的`createJavaBeanDeserializer`生成处理类。

## 处理类的处理流程

··暂略

# Fastjson gadget流程
纵观整个Fastjson处理流程，可以注意到对jsonstring的和兴处理流程是在`DefaultJSONParser#parse(Object fieldName)`中根据jsonstrinh的标志位来进行分发的，常见的有两种情况：

```json
  # 正常的kv结构
  {"k":"v"}

  # 嵌套结构
  {"k":{"kk":"vv","kk":"vv"},"k":{"k":"kk","kk":"vv","kk":"vv"}},k:v}
```

Fastjson的解析方式会首先判断当前标志位，这里拿完整的解析过程举个例子：

首先最开始解析的标志位为 `{`

   1. 判断下一个标志位是否为`"`，如果是`"`则提取key值，这时的标志位为`"`。
   2. 判断下一标志位是否为`:`
      - 如果为`:`则判断下一个标志位是否为`"`，如果是，则获取value值，这时的标志位为`"`。
      - 如果为`{`则重复1、2的过程。
   3. 判断下一个标志位是否为`}`
      - 如果为`}`则表示这一个单元的解析结束
      - 如果为`,`则表示要解析下一个kv的数据，重复1,2,3

更具不同的标志位进行不同的解析。当解析的过程中碰到了`@type`或`$ref`时，将当作特殊的标志做相应的处理。

# checkAutoType黑名单检测
当解析过程中找到了`@type`这个关键的标志时，将提取其所对应的值，并检测这个值是否在黑名单中：

`com.alibaba.fastjson.parser.DefaultJSONParser`
```java
if (key == JSON.DEFAULT_TYPE_KEY
        && !lexer.isEnabled(Feature.DisableSpecialKeyDetect)) {
    String typeName = lexer.scanSymbol(symbolTable, '"');

if (lexer.isEnabled(Feature.IgnoreAutoType)) {
    continue;
}

Class<?> clazz = null;
if (object != null
        && object.getClass().getName().equals(typeName)) {
    clazz = object.getClass();
} else {

boolean allDigits = true;
for (int i = 0; i < typeName.length(); ++i) {
    char c = typeName.charAt(i);
    if (c < '0' || c > '9') {
        allDigits = false;
        break;
    }
}

if (!allDigits) {
    clazz = config.checkAutoType(typeName, null, lexer.getFeatures());
    }
}
```

`com.alibaba.fastjson.parser.ParserConfig`
```java
if (!autoTypeSupport) {
    long hash = h3;
    for (int i = 3; i < className.length(); ++i) {
        char c = className.charAt(i);
        hash ^= c;
        hash *= PRIME;

    if (Arrays.binarySearch(denyHashCodes, hash) >= 0) {
        throw new JSONException("autoType is not support. " + typeName);
    }

// white list
if (Arrays.binarySearch(acceptHashCodes, hash) >= 0) {
    if (clazz == null) {
        clazz = TypeUtils.loadClass(typeName, defaultClassLoader, true);
    }

if (expectClass != null && expectClass.isAssignableFrom(clazz)){
    throw new JSONException("type not match. " + typeName + " -> " + expectClass.getName());
}

            return clazz;
        }
    }
}
```

先过黑名单再过白名单，这样保证了`@type`所引用的类是较为安全的。

# deserialze流程
jsonstring经过解析且经过安全性验证后，最终都要变成相应的对象，而变成对象的过程就是利用反射完成的，这个过程就是反序列化的过程。而该过程主要在`DefaultJSONParser#parseObject`中调用`deserializer.deserialze()`完成：

```java
ObjectDeserializer deserializer = config.getDeserializer(clazz);
Class deserClass = deserializer.getClass();
if (JavaBeanDeserializer.class.isAssignableFrom(deserClass)
        && deserClass != JavaBeanDeserializer.class
        && deserClass != ThrowableDeserializer.class) {
    this.setResolveStatus(NONE);
} else if (deserializer instanceof MapDeserializer) {
    this.setResolveStatus(NONE);
}
Object obj = deserializer.deserialze(this, clazz, fieldName);
return obj;
```

这里会根据`@type`所指定的类来获取或生成反序列化类，完成反序列化过程，这里如果是在预定数组中的类的话就可以直接调用相关类的`deserialze`方法完成反序列化操作

如果没有则会进入asm创建处理类的流程

# gadget执行的关键--反射调用
在具体进行反射前还有一个操作，将会解析看jsonstring中是否存在`val`字段，如果由，则将其提取出来赋给`objVal`，并将`objVal`的类名赋值给`strVal`

之后根据`clazz`类型交由不同的流程来处理

当`clazz`是一个class类型时，就会进入`TypeUtils.loadClass`中根据`strVal`进行类调用

```java
public static Class<?> loadClass(String className, ClassLoader classLoader,boolean cache) {
    if(className == null || className.length() == 0 || className.length() > 128){
        return null;
    }
    Class<?> clazz = mappings.get(className);
    if(clazz != null){
        return clazz;
    }
    if(className.charAt(0) == '['){
        Class<?> componentType = loadClass(className.substring(1), classLoader);
        return Array.newInstance(componentType, 0).getClass();
    }
    if(className.startsWith("L") && className.endsWith(";")){
        String newClassName = className.substring(1, className.length() - 1);
        return loadClass(newClassName, classLoader);
    }
    try{
        if(classLoader != null){
            clazz = classLoader.loadClass(className);
            if (cache) {
                mappings.put(className, clazz);
            }
            return clazz;
        }
    } catch(Throwable e){
        e.printStackTrace();
        // skip
    }
```

其中有两点是造成Fastjson两个rce的关键点

第一个点会对传入的`@type`的值进行解析，如果符合相应的格式则直接进行类加载

第二个点首先会反射调用`@type`的值所设置的类，然后将其加入到mappings中，当后面再次经过`checkAutoType`时，将会调用

首先从mappings中获取`typeName`相同的类，也就是说这里再进行黑名单检测前就已经返回了类，从而绕过了黑名单。

