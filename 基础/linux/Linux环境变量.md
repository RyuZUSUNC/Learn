# Ubuntu-18
示例

vim /etc/profile

在文件末尾添加
```shell
# JDK配置
JAVA_HOME=/private/java/jdk-16.0.1
export JAVA_HOME
export PATH=${PATH}:${JAVA_HOME}/bin
# maven配置
MAVEN_HOME=/private/java/apache-maven-3.8.1
export MAVEN_HOME
export PATH=${PATH}:${MAVEN_HOME}/bin
```

刷新环境变量

source /etc/profile