# 思路
使用java开发一项包含基础加解密，编码转换的图形界面工具。

# 包含
- MD5加密
- base64加解密
- ROT1-25
- 

# 整体布局
![](开发img\index.png)
>左侧panel使用Jtree做选择

>右侧panel为模块放置位置，在左侧选择后会显示相应模块

# 加密解密模块
## MD5加密模块
### 布局
![](开发img\MD5K.png)

### 实现过程
```java
    private MessageDigest mc = MessageDigest.getInstance("MD5");

    private void button1ActionPerformed(ActionEvent e) {
        // TODO add your code here
        String message = MD5Source.getText();//获取用户输入数值
        mc.update(message.getBytes());//MD5加密
        String a = new BigInteger(1, mc.digest()).toString(16);//将加密的byte形式的值转换成String方便输出
        MD5encode1.setText(a);//输出值
        MD5encode2.setText(a.toUpperCase());//大写输出值
    }//button事件
```

## base64加解密模块
### 布局
![](开发img\base64K.png)

### 实现过程
```java
private void base64decodeActionPerformed(ActionEvent e){
        // TODO add your code here
        byte[] bs64 = Base64.getDecoder().decode(base64code.getText());//获取用户输入字符通过base64加密，输出byte数组型值
        try {
            base64source.setText(new String(bs64,"utf-8"));//将byte数组转换成String输出
        } catch (UnsupportedEncodingException ex) {
            ex.printStackTrace();
        }
    }

    private void base64encodeActionPerformed(ActionEvent e){
        // TODO add your code here
        String bs = base64source.getText();//获取用户输入字符
        byte[] bytes = new byte[0];//定义一个比特数组
        try {
            bytes = bs.getBytes("utf-8");//将用户输入字符转换成byte（utf-8编码）
        } catch (UnsupportedEncodingException ex) {
            ex.printStackTrace();
        }
        String bss64 = Base64.getEncoder().encodeToString(bytes);//base64加密
        base64code.setText(bss64);//输出值
    }
```
>上方为输入框/原字符框
>
>下方为BASE64字符值框
>
>输入时必须按照字符类型输入对应的框

>注意在方法体必须要有try/cath时，写在事件中，写在自动生成代码中会被刷新掉。

## ROT1-25加密模块
### 布局
![](开发img\base64K.png)

### 实现过程
```java
    private void textArea4CaretUpdate(CaretEvent e) {
        // TODO add your code here
        String str = ROT13source.getText();//获取用户输入值
        String s = "";//定义空String值
        //System.out.println(ROT13CBOX.getSelectedIndex());
            for (int i = 0; i < str.length(); i++) {
                char c = str.charAt(i);//获取String字符中某一个位置的字符并赋值给c
                if ((c >= 'A') && (c <= 'Z')) {
                    c += ROT13CBOX.getSelectedIndex()+1;
                    if (c > 'Z')
                        c -= 26;
                } else if ((c >= 'a') && (c <= 'z')) {
                    c += ROT13CBOX.getSelectedIndex()+1;
                    if (c > 'z')
                        c -= 26;
                } else if ((c >= '0') && (c <= '9')) {
                    c += ROT13CBOX.getSelectedIndex()-8;
                    if (c > '9')
                        c -= 10;
                }
                s += String.valueOf(c);
            }//ROT算法，类似凯撒加密
            ROT13edcode.setText(s);//输出值
    }

    private void ROT13CBOXItemStateChanged(ItemEvent e) {
        // TODO add your code here
        ROT13source.setText("");//清空输入框
    }
```
>使用两个textarae和一个combobox实现的输入时即时加密/解密值

>使用textAreaCaretUpdate()触发器，在输入框更新时触发

>comboboxItemStateChanged()触发器，在combobox选中项更改时触发

