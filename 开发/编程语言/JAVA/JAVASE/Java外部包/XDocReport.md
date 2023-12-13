## 适用范围

XDocReport是一个用来进行文档填充和文档格式转换的java api。在一些项目中，我们可能需要对一份模板里的某些字段进行填充，比如电子合同中需要填写双方信息以及一些金额数据。这时候，我们就可以用XDocReport来实现我们的功能。如果需要把word文档转成pdf，也可以用XDocReport，但是其对中文支持不太好，可能需要用其它工具。

文档填充支持的格式包括`docx`和`odt`，`docx`可以使用Office创建和查看，odt可以使用openoffice和libreoffice创建和查看。两种文档在设计模板上会有些许不同，在代码上没有任何区别，下面会详细介绍。

## GitHub

https://github.com/opensagres/xdocreport

## 模板引擎

XDocReport使用的模板引擎是freemarker和velocity,官方教程大多数采用的是velocity（当然也有介绍freemarker）,但下面使用的是freemarker，二者的填充占位符有所不同。

## 填充字段设置

首先是字段占位符的设置。我们的文档是docx格式，用office打开后，在你需要填充的地方，先按`ctrl+f9`，是不是出现了一对有阴影的括弧？如果没出现，可能是因为开启了笔记本上F1-F12的快捷键。在括弧上右键，选择`“编辑域”`，然后选择`“MergeField”`(如果是中文的就找找看意思相近的，貌似是邮件合并)。接着在上面填写占位符，如果到时候在程序上选择freemarker模板引擎，那么占位符就是. . . , 占 位 符 里 填 写 占 位 的 字 符 串 。 如 果 是 v e l o c i t y 模 板 引 擎 , 那 么 占 位 符 就 是 {...},占位符里填写占位的字符串。如果是velocity模板引擎,那么占位符就是...,占位符里填写占位的字符串。如果是velocity模板引擎,那么占位符就是,然后后面填写占位的字符串。由于我打算用freemarker，所以可以从图片里看到，我的都是${…}。总结一下就是，ctrl+f9 -> 邮件编辑域 -> MergeField -> 填写占位符。

如果填充的文档是odt格式,那么只需要填写占位符就好了。

## java代码示例

```java
        //1.通过freemarker模板引擎加载文档，并缓存到registry中
        InputStream in = new FileInputStream("C:\\Users\\RyuZU\\Desktop\\周报20230424至20230501.docx");
        IXDocReport report = XDocReportRegistry.getRegistry().loadReport(in, TemplateEngineKind.Freemarker);

        //2.设置填充字段、填充类以及是否为list。
        FieldsMetadata fieldsMetadata = report.createFieldsMetadata();
        fieldsMetadata.load("Tset", Test.class);
        report.setFieldsMetadata(fieldsMetadata);

        //3.模拟填充数据
        Test test = new Test("CEST","CCCC");

        //4.匹配填充字段和填充数据，进行填充
        IContext context = report.createContext();
        context.put("Test",test);
        OutputStream out = new FileOutputStream(
                new File("C:\\Users\\RyuZU\\Desktop\\周报20230424至20230501-T.docx"));
        report.process(context,out);
```