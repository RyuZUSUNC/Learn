## 提取音频
ffmpeg -i input.flv -vn -codec copy out.m4a

>-i的意思是input，后接输入源。-codec的意思是直接复制流。

