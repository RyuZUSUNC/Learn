# 安装

## Ubuntu

- sudo apt update //更新软件包缓存
- sudo apt install docker //安装docker
- sudo servie docker start //启动docker

# 指令集

## 容器生命周期管理

### run
    语法
    docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
- docker run ：创建一个新的容器并运行一个命令
    - -a stdin: 指定标准输入输出内容类型，可选 STDIN/STDOUT/STDERR 项；
    - -d: 后台运行容器，并返回容器ID；
    - -i: 以交互模式运行容器，通常与 -t 同时使用；
    - -P: 随机端口映射，容器内部端口随机映射到主机的高端口
    - -p: 指定端口映射，格式为：主机(宿主)端口:容器端口
    - -t: 为容器重新分配一个伪输入终端，通常与 -i 同时使用；
    - --name="nginx-lb": 为容器指定一个名称；
    - --dns 8.8.8.8: 指定容器使用的DNS服务器，默认和宿主一致；
    - --dns-search example.com: 指定容器DNS搜索域名，默认和宿主一致；
    - -h "mars": 指定容器的hostname；
    - -e username="ritchie": 设置环境变量；
    - --env-file=[]: 从指定文件读入环境变量；
    - --cpuset="0-2" or --cpuset="0,1,2": 绑定容器到指定CPU运行；
    - -m :设置容器使用内存最大值；
    - --net="bridge": 指定容器的网络连接类型，支持 bridge/host/none/    container: 四种类型；
    - --link=[]: 添加链接到另一个容器；
    - --expose=[]: 开放一个端口或一组端口；
    - --volume , -v:	绑定一个卷

### start/stop/restart
    语法
    docker start [OPTIONS] CONTAINER [CONTAINER...]
    docker stop [OPTIONS] CONTAINER [CONTAINER...]
    docker restart [OPTIONS] CONTAINER [CONTAINER...]
- docker start :启动一个或多个已经被停止的容器
- docker stop :停止一个运行中的容器
- docker restart :重启容器

### update
- docker update :更新一个运行中的容器的配置
  - docker update --restart=always <container_id> ：设置 restart policy: always 自动重启容器

### kill
    语法
    docker kill [OPTIONS] CONTAINER [CONTAINER...]
- docker kill :杀掉一个运行中的容器。
    - -s :向容器发送一个信号

### rm
    语法
    docker rm [OPTIONS] CONTAINER [CONTAINER...]
- docker rm ：删除一个或多少容器
    - -f :通过SIGKILL信号强制删除一个运行中的容器
    - -l :移除容器间的网络连接，而非容器本身
    - -v :-v 删除与容器关联的卷

### pause/unpause
    语法
    docker pause [OPTIONS] CONTAINER [CONTAINER...]
    docker unpause [OPTIONS] CONTAINER [CONTAINER...]
- docker pause :暂停容器中所有的进程。
- docker unpause :恢复容器中所有的进程。

### create
    语法
    docker create [OPTIONS] IMAGE [COMMAND] [ARG...]
- docker create ：创建一个新的容器但不启动它

### exec
    语法
    docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
- docker exec ：在运行的容器中执行命令
    - -d :分离模式: 在后台运行
    - -i :即使没有附加也保持STDIN 打开
    - -t :分配一个伪终端
> 例：sudo docker exec -it `7752222e1e1` /bin/bash

## 容器操作

### ps
    语法
    docker ps [OPTIONS]
- docker ps : 列出容器
    - -a :显示所有的容器，包括未运行的。
    - -f :根据条件过滤显示的内容。
    - --format :指定返回值的模板文件。
    - -l :显示最近创建的容器。
    - -n[number] :列出最近创建的n个容器。
    - --no-trunc :不截断输出。
    - -q :静默模式，只显示容器编号。
    - -s :显示总的文件大小。

### inspect
    语法
    docker inspect [OPTIONS] NAME|ID [NAME|ID...]
- docker inspect : 获取容器/镜像的元数据。
    - -f :指定返回值的模板文件。
    - -s :显示总的文件大小。
    - --type :为指定类型返回JSON。

### top
    语法
    docker top [OPTIONS] CONTAINER [ps OPTIONS]
>容器运行时不一定有/bin/bash终端来交互执行top命令，而且容器还不一定有top命令，可以使用docker top来实现查看container中正在运行的进程。
- docker top :查看容器中运行的进程信息，支持 ps 命令参数。

### attach
    语法
    docker attach [OPTIONS] CONTAINER
- docker attach :连接到正在运行中的容器。
>要attach上去的容器必须正在运行，可以同时连接上同一个container来共享屏幕（与screen命令的attach类似）。

>官方文档中说attach后可以通过CTRL-C来detach，但实际上经过我的测试，如果container当前在运行bash，CTRL-C自然是当前行的输入，没有退出；如果container当前正在前台运行进程，如输出nginx的access.log日志，CTRL-C不仅会导致退出容器，而且还stop了。这不是我们想要的，detach的意思按理应该是脱离容器终端，但容器依然运行。好在attach是可以带上--sig-proxy=false来确保CTRL-D或CTRL-C不会关闭容器。


### events
    语法
    docker events [OPTIONS]
- docker events : 从服务器获取实时事件
    - -f ：根据条件过滤事件；
    - --since ：从指定的时间戳后显示所有事件;
    - --until ：流水时间显示到指定的时间为止；

### logs
    语法
    docker logs [OPTIONS] CONTAINER
- docker logs : 获取容器的日志
    - -f : 跟踪日志输出
    - --since :显示某个开始时间的所有日志
    - -t : 显示时间戳
    - --tail :仅列出最新N条容器日志

### wait
    语法
    docker wait [OPTIONS] CONTAINER [CONTAINER...]
- docker wait : 阻塞运行直到容器停止，然后打印出它的退出代码。


### export
    语法
    docker export [OPTIONS] CONTAINER
- docker export :将文件系统作为一个tar归档文件导出到STDOUT。
    - -o :将输入内容写到文件。

### port
    语法
    docker port [OPTIONS] CONTAINER [PRIVATE_PORT[/PROTO]]
- docker port :列出指定的容器的端口映射，或者查找将PRIVATE_PORT NAT到面向公众的端口。

## 容器rootfs命令

### commit
    语法
    docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
- docker commit :从容器创建一个新的镜像。
    - -a :提交的镜像作者；
    - -c :使用Dockerfile指令来创建镜像；
    - -m :提交时的说明文字；
    - -p :在commit时，将容器暂停。

### cp
    语法
    docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-
    docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH
- docker cp :用于容器与主机之间的数据拷贝。
    - -L :保持源目标中的链接

### diff
    语法
    docker diff [OPTIONS] CONTAINER
- docker diff : 检查容器里文件结构的更改。

## 镜像仓库

### login
    语法
    docker login [OPTIONS] [SERVER]
    docker logout [OPTIONS] [SERVER]
- docker login : 登陆到一个Docker镜像仓库，如果未指定镜像仓库地址，默认为官方仓库 Docker Hub
- docker logout : 登出一个Docker镜像仓库，如果未指定镜像仓库地址，默认为官方仓库 Docker Hub
    - -u :登陆的用户名
    - -p :登陆的密码

### pull
    语法
    docker pull [OPTIONS] NAME[:TAG|@DIGEST]
- docker pull : 从镜像仓库中拉取或者更新指定镜像
   - -a :拉取所有 tagged 镜像
   - --disable-content-trust :忽略镜像的校验,默认开启

### push
    语法
    docker push [OPTIONS] NAME[:TAG]
- docker push : 将本地的镜像上传到镜像仓库,要先登陆到镜像仓库
    - --disable-content-trust :忽略镜像的校验,默认开启

### search
    语法
    docker search [OPTIONS] TERM
- docker search : 从Docker Hub查找镜像
   - --automated :只列出 automated build类型的镜像；
   - --no-trunc :显示完整的镜像描述；
   - -s :列出收藏数不小于指定值的镜像。

## 本地镜像管理

### images
    语法
    docker images [OPTIONS] [REPOSITORY[:TAG]]
- docker images : 列出本地镜像。
    - -a :列出本地所有的镜像（含中间映像层，默认情况下，过滤掉中间映像层）；
    - --digests :显示镜像的摘要信息；
    - -f :显示满足条件的镜像；
    - --format :指定返回值的模板文件；r
    - --no-trunc :显示完整的镜像信息；
    - -q :只显示镜像ID。

### rmi
    语法
    docker rmi [OPTIONS] IMAGE [IMAGE...]
- docker rmi : 删除本地一个或多少镜像。
    - -f :强制删除；
    - --no-prune :不移除该镜像的过程镜像，默认移除；

### tag
    语法
    docker tag [OPTIONS] IMAGE[:TAG] [REGISTRYHOST/][USERNAME/]NAME[:TAG]
- docker tag : 标记本地镜像，将其归入某一仓库。

### build
    语法
    docker build [OPTIONS] PATH | URL | -
- docker build 命令用于使用 Dockerfile 创建镜像。
    - --build-arg=[] :设置镜像创建时的变量；
    - --cpu-shares :设置 cpu 使用权重；
    - --cpu-period :限制 CPU CFS周期；
    - --cpu-quota :限制 CPU CFS配额；
    - --cpuset-cpus :指定使用的CPU id；
    - --cpuset-mems :指定使用的内存 id；
    - --disable-content-trust :忽略校验，默认开启；
    - -f :指定要使用的Dockerfile路径；
    - --force-rm :设置镜像过程中删除中间容器；
    - --isolation :使用容器隔离技术；
    - --label=[] :设置镜像使用的元数据；
    - -m :设置内存最大值；
    - --memory-swap :设置Swap的最大值为内存+swap，"-1"表示不限swap；
    - --no-cache :创建镜像的过程不使用缓存；
    - --pull :尝试去更新镜像的新版本；
    - --quiet, -q :安静模式，成功后只输出镜像 ID；
    - --rm :设置镜像成功后删除中间容器；
    - --shm-size :设置/dev/shm的大小，默认值是64M；
    - --ulimit :Ulimit配置。
    - --tag, -t: 镜像的名字及标签，通常 name:tag 或者 name 格式；可以在一次构建中为一个镜像设置多个标签。
    - --network: 默认 default。在构建期间设置RUN指令的网络模式

### history
    语法
    docker history [OPTIONS] IMAGE
- docker history : 查看指定镜像的创建历史。
    - -H :以可读的格式打印镜像大小和日期，默认为true；
    - --no-trunc :显示完整的提交记录；
    - -q :仅列出提交记录ID。

### save
    语法
    docker save [OPTIONS] IMAGE [IMAGE...]
- docker save : 将指定镜像保存成 tar 归档文件。
    - -o :输出到的文件。

### load
    语法
    docker load [OPTIONS]
- docker load : 导入使用 docker save 命令导出的镜像。
    - -i :指定导出的文件。
    - -q :精简输出信息。

### import
    语法
    docker import [OPTIONS] file|URL|- [REPOSITORY[:TAG]]
- docker import : 从归档文件中创建镜像。
    - -c :应用docker 指令创建镜像；
    - -m :提交时的说明文字；

## info|version

### info
    语法
    docker info [OPTIONS]
- docker info : 显示 Docker 系统信息，包括镜像和容器数。。

### version
    语法
    docker version [OPTIONS]
- docker version :显示 Docker 版本信息。
    - -f :指定返回值的模板文件。

## 镜像制作
### 将容器变为镜像
- docker commit 261314c94305 imagexxx
可用参数
-a :提交的镜像作者；
-c :使用Dockerfile指令来创建镜像；
-m :提交时的说明文字；
-p :在commit时，将容器暂停。
imagexxx 是新创建的镜像的名字

### 将镜像打包成tar包
- docker  save  -o xxx.tar  imagexxx # 当前路径下会生成一个xxx.tar

### 将tar包再次压缩为gz包
- tar -zcvf xxx.tar.gz     xxx.tar    # 当前路径生成一个xxx.tar.gz压缩包

### 将tar.gz 解压缩，会生成一个tar包
- tar -zxvf xxx.tar.gz

### 将tar包生成镜像
docker  load  <  xxx.tar     # 生成的镜像跟之前打包的镜像名称一样



docker run -d -p 5001:22 ssh-ubuntu /usr/sbin/sshd -D

(-p为端口映射 容器中22端口应射程主机5001端口  ||   /usr/sbin/sshd -D是指定容器启动后要运行的command，本处是启动ssh服务)

