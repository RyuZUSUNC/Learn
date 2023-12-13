# 配置GO环境
- File -> Setting -> GO -> GOROOT

配置GOROOT，一般自动会联想出来，选择即可。

- File -> Setting -> GO -> GOPATH

GOPATH最好每个project单独设置，不使用默认系统环境的 GOPATH 作为 GOPATH 不勾选`Use GOPATH that's defined in system environment`。同时GOPATH的设定是src目录的上级目录。

# 设置GIT
- File -> Setting -> Version Control -> Git

一般装了git的会自动填入git路径，用于go get拉取第三方代码库。

# SSH
- Tools -> Start SSH session...

goland自带ssh连接，不用再单独安装SecureCRT，putty等工具了‘

可以右键最下方的terminal标签设置View Mode，这样鼠标点击代码区域时，这个terminal自动最小化。

- File -> Setting -> Tools -> SSH Terminal

SSH默认是GBK编码，如果出现乱码，可以改为UTF-8编码，但是改完要重新连接。

# REST Client
- Tools -> HTTP Client

Goland自带REST测试客户端，可以省去再安装postman，curl等工具。

# FTP
- Tools -> Deployment -> Configuration...

goland自带ftp功能，不需要再单独安装xftp等工具（当然也没有xftp强大，基本使用是够了）。

# Database连接
- View -> Tool Windows -> Database

略，就是一般的 JB_IDE 的连接配置，但是每种数据库都要先下载其对应的驱动器。

如果是手动下载的，将下载后的jar包放到goland的安装目录里面找个位置，然后点击Go to Driver，选择自定义驱动，然后选择刚才下载的那个jar包即可。

# 代码视图
- View -> Appearance

有的时候为了方便看代码，可以试试这四种方式

# 配置编译
- Run -> Edit Configurations... -> + -> Go Build

1. 名称：为本条配置信息的名称，可以自定义，也可以使用系统默认的值，这个就是编译后程序的名称
2. Run kind：这里需要设置为“Directory”；
3. Directory：用来设置 main 包所在的目录，不能为空；
4. Output directory：用来设置编译后生成的可执行文件的存放目录，可以为空，为空时默认不生成可执行文件；
5. Working directory：用来设置程序的运行目录，可以与“Directory”的设置相同，但是不能为空。