# JDK9
```java
public class NineNewTest {
 
    /**不可变集合工厂方法
     * Java 9增加了List.of()、Set.of()、Map.of()和Map.ofEntries()等工厂方法来创建不可变集合。
     * List strs = List.of("Hello", "World");
     * List strs List.of(1, 2, 3);
     * Set strs = Set.of("Hello", "World");
     * Set ints = Set.of(1, 2, 3);
     * Map maps = Map.of("Hello", 1, "World", 2);
    **/
    public static void testFinalCollections(){
        List<String> aaa = List.of("aaa", "bbb");
        Map<String, Integer> hello = Map.of("Hello", 1, "World", 2);
        System.out.println(aaa.toString());
        System.out.println(hello);
    }
 
    /**
     * I/O 流新特性
     * java.io.InputStream 中增加了新的方法来读取和复制 InputStream 中包含的数据。
     *    readAllBytes：读取 InputStream 中的所有剩余字节。
     *    readNBytes： 从 InputStream 中读取指定数量的字节到数组中。
     *    transferTo：读取 InputStream 中的全部字节并写入到指定的 OutputStream 中
    **/
    public void testIO(){
        try(InputStream resourceAsStream = this.getClass().getResourceAsStream("1.txt");
        OutputStream outputStream = new FileOutputStream(new File("d:\\2.txt"))) {
            // InputStream stream = new BufferedInputStream(resourceAsStream);
            byte[] bytes;
            // bytes  = resourceAsStream.readAllBytes();
            // bytes = resourceAsStream.readNBytes(10);
            resourceAsStream.transferTo(outputStream);
            // System.out.println(new String(bytes));
            outputStream.close();
        }catch (IOException e){
            e.printStackTrace();
        }
    }
 
 
 
    public static void main(String[] args) throws IOException {
        // NineNewTest.testFinalCollections();
        NineNewTest test = new NineNewTest();
        test.testIO();
    }
}
```

# JDK10
```java
 /**
 * DK10中包含许多对JVM的优化：
 *
 *    将JDK多存储库合并为单存储库
 *    并行Full GC 的G1
 *    垃圾回收接口
 *    应用数据共享
 *    线程局部管控
 *    基于实验JAVA 的JIT 编译器
 *    备用内存设备上分配堆内存
 **/
public class TenNewTest {
 
    /**
     * 局部变量类型推断可以说是Java 10中最值得注意的特性，这是Java语言开发人员为了简化Java应用程序的编写而采取的又一步，如下图所示。
     * 局部变量类型推荐仅限于如下使用场景：
     *
     * 局部变量初始化
     *    for循环内部索引变量
     *    传统的for循环声明变量
     *    Java官方表示，它不能用于以下几个地方：
     *
     * 方法参数
     *    构造函数参数
     *    方法返回类型
     *    字 段
     *    捕获表达式（或任何其他类型的变量声明）
    **/
    public static void main(String[] args) {
 
        var sds = List.of("sds", "ccd", "sds");
        System.out.println(sds.toString());
    }
}
```

# JDK11
```java
public class ElevenNewTest {
 
    /**
     * HTTPClient转正
     * JDK9中便引入httpclient模块，但它在jdk.incubator.httpclient包下，在java11被标记为正式，改为java.net.http模块。
     **/
    public static void httpTest() throws IOException, InterruptedException {
        HttpClient client = HttpClient.newBuilder()
                .version(HttpClient.Version.HTTP_2) // .version(HttpClient.Version.HTTP_1_1)
                .connectTimeout(Duration.ofMillis(5000)) // 连接超时时间，单位为毫秒
                .followRedirects(HttpClient.Redirect.NEVER)  // 连接完成之后的转发策略
                //.executor(Executors.newFixedThreadPool(5)) // 线程池
                //认证，默认情况下 Authenticator.getDefault() 是 null 值，会报错
                //.authenticator(Authenticator.getDefault())
                //代理地址
                //.proxy(ProxySelector.of(new InetSocketAddress("http://www.baidu.com", 8080)))
                //缓存，默认情况下 CookieHandler.getDefault() 是 null 值，会报错
                //.cookieHandler(CookieHandler.getDefault())
                .build();
        HttpRequest request = HttpRequest.newBuilder()//存入消息头
                //消息头是保存在一张 TreeMap 里的
                .header("Content-Type", "application/json")
                //http 协议版本
                .version(HttpClient.Version.HTTP_2)
                //url 地址
                //.uri(URI.create("http://openjdk.java.net/"))
                .uri(URI.create("https://www.baidu.com/"))
                //超时时间
                .timeout(Duration.ofMillis(5009))
                //发起一个 post 消息，需要存入一个消息体
                //.POST(HttpRequest.BodyPublishers.ofString("hello"))
                //发起一个 get 消息，get 不需要消息体
                .GET()
                //method(...) 方法是 POST(...) 和 GET(...) 方法的底层，效果一样
                //.method("POST",HttpRequest.BodyPublishers.ofString("hello"))
                //创建完成
                .build();
 
        HttpResponse<String> response =
                client.send(request, HttpResponse.BodyHandlers.ofString());
        System.out.println(response.body());
 
//         try {
//             //返回的是 future，然后通过 future 来获取结果
//             CompletableFuture<String> future =
//                     client.sendAsync(request, HttpResponse.BodyHandlers.ofString())
//                             .thenApply(HttpResponse::body);
//             //阻塞线程，从 future 中获取结果
//             String body = future.get();
//         } catch (ExecutionException e) {
//             e.printStackTrace();
//         }
 
 
    }
 
    /** *
     * 更灵活的String
     * 去除空白
     * JAVA11(JDK11)中的strip()方法，适用于字符首尾空白是Unicode空白字符的情况
     * trim()方法移除字符串两侧的空白字符(空格、tab键、换行符)
     * 支持Unicode的空白字符的判断应该使用isWhitespace(int)。
     * 此外，开发人员无法专门删除缩进空白或专门删除尾随空白。
     * 简单得说就是，trim()方法无法删除掉Unicode空白字符，但用Character.isWhitespace©方法可以判断出来。
     *
     * String text = "  \u2000a  b  ";
     * Assert.assertEquals("a  b",text.strip());
     * Assert.assertEquals("\u2000a  b",text.trim());
     * Assert.assertEquals("a  b  ",text.stripLeading());
     * Assert.assertEquals("  \u2000a  b",text.stripTrailing());
     *
     *
     * lines()
     * 字符串实例方法，使用专门的 Spliterator 来懒惰地提供源字符串中的行
     * "test\nhoge\n".lines().map(String::toUpperCase).toArray()
     * 输出： Object[2] { "TEST", "HOGE" }
     *
     * repeat(int)
     * 按照参数 int 提供的次数来重复字符串的运行次数
     *
     * isBlank()
     * 验证当前字符串是否为空，或者是否只包括空白字符（空白字符由 Character.isWhiteSpace(int) 验证）
    **/
    public static void stringNewTest(){
        String text = "  \u2000a  b  ";
        System.out.println("a  b".equals(text.strip()));
        System.out.println("\u2000a  b".equals(text.trim()));
        System.out.println("a  b  ".equals(text.stripLeading()));
        System.out.println("  \u2000a  b".equals(text.stripTrailing()));
 
        var objects = "test\nhoge\n".lines().map(String::toUpperCase).toArray();
        System.out.println(objects[0].toString() + " : " + objects[1].toString());
 
        System.out.println("test\n".repeat(3));
 
        System.out.println("".isBlank());
        System.out.println("\\u0020".isBlank());
        System.out.println("\\u3000".isBlank());
 
    }
 
    public static void main(String[] args) throws IOException, InterruptedException {
        // ElevenNewTest.httpTest();
 
        ElevenNewTest.stringNewTest();
    }
 
}
```

# JDK12
```java
public class TwelveNewTest {
 
    private static final int MONDAY = 1;
    private static final int TUESDAY = 2;
    private static final int WEDNESDAY = 3;
    private static final int THURSDAY = 4;
    private static final int FRIDAY = 5;
    private static final int SATURDAY = 6;
    private static final int SUNDAY = 7;
    /**
     * switch语句
    **/
    public static void switchTest() {
        var day = 2;
        switch (day) {
            case MONDAY, FRIDAY, SUNDAY -> System.out.println(6);
            case TUESDAY -> System.out.println(7);
            case THURSDAY, SATURDAY -> System.out.println(8);
            case WEDNESDAY -> System.out.println(9);
            default -> System.out.println(0);
        }
 
        System.out.println(switch (day) {
            case MONDAY, FRIDAY, SUNDAY -> 6;
            case TUESDAY -> 7;
            case THURSDAY, SATURDAY -> 8;
            case WEDNESDAY -> 9;
            default -> -1;
        });
    }
 
    /**
     * 数字转字符串NumberFormat
    **/
    public static void numberFormatTest(){
        var cnf = NumberFormat.getCompactNumberInstance(Locale.CHINA, NumberFormat.Style.SHORT);
        System.out.println(cnf.format(1_0000));
        System.out.println(cnf.format(1_9200));
        System.out.println(cnf.format(1_000_000));
        System.out.println(cnf.format(1L << 30));
        System.out.println(cnf.format(1L << 40));
        System.out.println(cnf.format(1L << 50));
        System.out.println(NumberFormat.getCompactNumberInstance(Locale.CHINA, NumberFormat.Style.SHORT).format(12345));
        System.out.println(NumberFormat.getCompactNumberInstance(Locale.CHINA, NumberFormat.Style.LONG).format(1999999));
    }
 
    public static void testNewStringFuction(){
 
        System.out.println("eric".transform(new Function<String, Object>() {
            @Override
            public Object apply(String s) {
                return s + " " + s.hashCode();
            }
 
            @Override
            public <V> Function<V, Object> compose(Function<? super V, ? extends String> before) {
                return null;
            }
 
            @Override
            public <V> Function<String, V> andThen(Function<? super Object, ? extends V> after) {
                return null;
            }
        }));
 
        System.out.println("hello".indent(3));
    }
 
    public static void main(String[] args) {
 
        // TwelveNewTest.switchTest();
 
        // TwelveNewTest.numberFormatTest();
        TwelveNewTest.testNewStringFuction();
    }
}
```