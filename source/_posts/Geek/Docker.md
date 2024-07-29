---
title: Docker
tags: Docker
categories: Geek
abbrlink: f5f9fa9b
date: 2023-11-30 14:12:00
---
# 一些网站
教程网站:[狂神说JAVA Docker最新超详细版教程通俗易懂](https://www.bilibili.com/video/BV1og4y1q7M4/?p=1&vd_source=b1de3fe38e887eb40fc55a5485724480)
linux命令搜索网站: https://www.yiibai.com/linux/ps.html
vim编辑器的使用:https://www.runoob.com/linux/linux-vim.html

# 2023/12/20更新: 使用WSL在Windows上安装Linux
## 为什么使用WSL
通过虚拟机安装linux无法使用本机的gpu,对于一些需要gpu的开源项目无法很好的支持.因此改用WSL在Windows上安装Linux.
这样传文件,开发,都更加方便.
## WSL的安装步骤
文档参考:https://learn.microsoft.com/zh-cn/windows/wsl/setup/environment
前提:安装过程需要科学上网,配置清华镜像加速自行查阅.必须运行 Windows 10 版本 2004 及更高版本（内部版本 19041 及更高版本）或 Windows 11 才能使用以下命令。如果用的更早的版本,需要自行手动安装.

1. 右键通过管理员模式启动PowerShell或Windows命令提示符
2. 安装wsl和Ubuntu
```PowerShell
wsl --install
wsl --install Ubuntu
```
3. 重启计算机会自动进入Ubuntu,自行设置账号与密码
![Alt text](image-14.png)
4. 更新和升级包
```shell
sudo apt update && sudo apt upgrade
```
## vscode与wsl配合使用
文档参考:https://learn.microsoft.com/zh-cn/windows/wsl/tutorials/wsl-vscode
1. 更新Ubuntu,添加wget和ca证书.
```shell
sudo apt-get update
sudo apt-get install wget ca-certificates
```
2. 在wsl中通过vscode打开项目
```shell
code .
```
3. 下载wsl扩展
下载好以后可以通过左下角与wsl进行连接
![Alt text](image-15.png)
也可以新建终端,通过shell进行调试
![Alt text](image-16.png)

## 使用Docker
文档参考:https://learn.microsoft.com/zh-cn/windows/wsl/tutorials/wsl-containers
**通过文档参考中得到的可以查阅的网站:**
Docker的介绍文档:https://learn.microsoft.com/zh-cn/training/modules/intro-to-docker-containers/
在Windows上安装Docker桌面:https://docs.docker.com/desktop/install/windows-install/
在vscode中安装Dev Containers:https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers
在vscode中安装Docker:https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker

## WSL的一些好用命令
WSL（Windows Subsystem for Linux）发行版是指在 Windows 上运行的 Linux 操作系统版本。每个 WSL 发行版都包含了一个完整的用户模式环境，就像真实运行的 Linux 一样，可以支持大多数原生 Linux 应用和工具。

```shell
# 列出所有wsl发行版
wsl -l -v
# 导出一份wsl发行版(文件会放到用户文件夹中):
wsl --export Ubuntu 备份名字.tar
# 导入wsl发行版文件
wsl --import 新名称 存储新发行版的系统目录 导入的wsl文件名称.tar
# 进入某一个wsl发行版
wsl -d 环境名
# 关闭某一个wsl发行版(释放资源)(需要在shell中使用exit命令)
wsl --terminate 环境名
# 删除某一个wsl发行版
wsl --unregister 环境名 

```
# Docker的作用
> Docker是一种轻量级的虚拟化技术，同时是一个开源的应用容器运行环境搭建平台，可以让开发者以便捷方式打包应用到一个可移植的容器中，然后安装至任何运行Linux或Windows等系统的服务器上。相较于传统虚拟机，Docker容器提供轻量化的虚拟化方式、安装便捷、启停速度快。
 
# Docker的名词介绍
![Alt text](image.png)
**镜像(image)**:通过镜像可以创建多个容器
**容器(container)**:Docker创建出来的携带环境的应用,是通过镜像创建的
**仓库(repository)**:存放镜像的地方,分为公有仓库和私有仓库

# 从零开始安装Docker的过程
1. 前往官网安装VMWareWorkstation: https://www.vmware.com/cn/products/workstation-player.html
2. 安装linux(centos):https://www.cnblogs.com/Dengv5/p/16386206.html
3. 安装xshell(负责在本机操控linux):https://www.xshell.com/zh/free-for-home-school/
4. 将xshell与虚拟机的linux进行连接:https://www.xshellcn.com/zhishi/guanli-xuniji.html
5. Docker的安装:https://docs.docker.com/engine/install/centos/
6. 可选: DBeaver的安装(windows版即可,这个软件可以用来可视化查看数据库):https://dbeaver.io/download/

# Docker的常用命令
Docker的帮助文档地址:https://docs.docker.com/reference/
什么是shell,bash,sh:https://blog.csdn.net/wht1995316/article/details/115837282
## 重启Docker服务
```shell
# 重启DOcker
sudo systemctl restart docker
# 重启containerd
sudo systemctl restart containerd
```
## 帮助命令
```shell
docker version # 显示docker的版本信息
docker info # 显示docker的系统信息,包括镜像和容器的数量
docker 命令名字 --help # 帮助命令
```
## 镜像命令
```shell
docker images # 查看所有本地的主机上的镜像
docker images -q # 查看所有镜像ID

docker search 镜像名 # 搜索镜像
docker pull 镜像名 # 下载镜像
docker pull 镜像名:镜像版本号 # 下载对应版本镜像

docker rmi -f 镜像id  #删除指定id的镜像
docker rmi -f 镜像id 镜像id 镜像id # 批量删除指定id镜像
docker rmi -f $(docker images -aq) # 删除全部镜像
```
## 容器命令
```shell
# 创建并启动容器
docker run -it 镜像名字 /bin/bash # 以bash的交互方式创建容器 -it意思是后面可以跟一个命令,这里跟/bin/bash意思是以bash方式进入容器
# 后台启动容器
docker run -d 镜像名字 # 后台创建容器,如果容器发现没有应用就会自动停止
# 查询容器
docker ps # 列出当前正在运行的容器
docker ps -a # 列出当前正在运行的容器加上历史运行过的容器
docker ps -n=数字 # 列出最近创建的对应数字的容器
docker ps -q # 
# 退出容器
exit # 停止容器并退出
快捷键:ctrl+p+q # 退出但不停止容器
# 删除容器
docker rm 容器id # 删除容器
docker rm -f 容器id # 强制删除容器
docker rm -f $(docker ps -aq) # 强制删除所有容器
# 启动和停止已经创建好的容器
docker start 容器id # 可以通过这个命令将之前退出的容器重新启动
docker restart 容器id # 重启容器
docker stop 容器id # 停止当前正在运行的容器
docker kill 容器id # 强制停止当前容器
# 查看日志
docker logs -tf --tail 查看日志条数 容器id # 查看日志
# 查看容器中进程信息
docker top 容器id
# 查看容器的元数据
docker inspect 容器id # 查看容器的元数据
# 进入当前正在运行的容器
docker exec -it 容器id /bin/bash # 进入容器后开启一个新的终端,可以在里面操作(常用)
docker attach 容器id # 进入容器正在执行的终端,不会启动新的进程
# 将容器的文件拷贝到主机上
docker cp 容器id:容器内的文件路径 要拷贝到的主机文件路径
```
# 测试1:部署Nginx
步骤:
1. 搜索镜像 docker search,虽然有命令,但更推荐前往dockerhub去搜索,里面内容更详细.[dockerhub链接](https://hub.docker.com/)
2. 下载镜像 docker pull 镜像名 或者 docker pull 镜像名:版本号
3. 查看镜像是否下载成功,docker images 查看所有已经下载的镜像
4. 创建容器, docker run -d --name 容器名 -p 宿主机的端口号:容器的端口号 镜像名
举例: docker run -d --name nginx01 -p 3344:80 nginx
5. curl localhost:宿主机端口号 # 在linux中测试访问域名
6. 通过xshell窗口上显示的192.168.***然后冒号端口号,进行浏览器上的访问
![Alt text](image-1.png)
# 测试2:部署Tomcat
```shell
# 官方的使用
docker run -it --rm tomcat:9.0 # 这里如果找不到tomcat镜像会自动下载,之前的启动都是后台,停止了容器之后,容器还是可以查到,加了--rm一般用来测试,因为退出容器后就自动删除了,查不到容器.
# 如果 docker run 没有自动下载,就docker pull 去下载
# 运行完以后可以使用ctrl+c或者ctrl+p+q退出

# 下载最新版本tomcat
docker pull tomcat
# 创建并运行容器,提供公网访问端口,给容器取别名叫tomcat01,容器对应端口号可以通过docker ps 来查看
docker run -d -p 3355:8080 --name tomcat01 tomcat # docker run -d -p 本机提供端口号:容器对应端口号 --name 容器名字 镜像名字
# 进入容器
docker exec -it tomcat01 /bin/bash
# 测试本地访问
curl localhost:端口号
# 测试网站访问
通过xshell窗口上显示的192.168.***然后冒号端口号,进行浏览器上的访问
# 发现显示404
# 在容器中使用 docker ls 列出容器的文件结构
# 发现webapps里没有文件,但是webapps.dist中有文件

# 将webapps.dist中的文件复制到webapps中
cp -r webapps.dist/* webapps
# 测试浏览器访问,正常显示了.
```
# Portainer可视化面板安装
Portainer介绍: Docker图形化界面管理工具,提供一个后台面板来进行操作.
安装与运行:(8088是提供的让外网访问的端口号)
```shell
docker run -d -p 8088:9000 \
--restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer
```
访问测试:
通过地址进入网站以后注册账号后得到的界面:
![Alt text](image-2.png)
# 镜像原理之联合文件系统
## 镜像是什么
> 镜像是一种轻量级,可执行的独立软件包,用来打包软件运行环境和基于运行环境开发的软件,它包含运行某个软件所需的所有内容,包括代码,运行时,库,环境变量和配置文件.
所有的应用,直接打包docker镜像,就可以直接跑起来.
**如何得到镜像**:
>- 从远程仓库下载
>- 朋友拷贝给你
>- 自己制作一个镜像DockerFile
## UnionFS(联合文件系统)
> 我们下载的时候看到的一层层就是这个!
UnionFS(联合文件系统):Union文件系统(UnionFS)是一种分层、轻量级并目高性能的文件系统，它支持对文件系统的修改作为一次提交来一层层的叠加，同时可以将不同目录挂载到同一个虚拟文件系统下(unite several diretories into a single virtualfilesystem)。Union 文件系统是 Docker 像的基础。镜像可以通过分层来进行继承，基于基础像(没有像 )可以制作各种具体的应用镜像。
特性:一次同时加载多个文件系统，但从外面看起来，只能看到一个文件系统，联合加载会把各层文件系统叠加起来，这样最终的文件系统会包含所有底层的文件和目录
## Docker镜像加载原理
> docker的镜像实际上由一层一层的文件系统组成,这种层级的文件系统叫UnionFS.
bootfs(boot file system)主要包含bootloader和kernel, bootloader主要是引导加载kernel,Linux刚启动时会加载bootfs文件系统，在Docker镜像的最底层是bootfs。这一层与我们典型的Linux/Unix系统是一样的，包含boot加载器和内核。当boot加载完成之后整个内核就都在内存中了，此时内存的使用权已由bootfs转交给内核，此时系统也会卸载bootfs。
rootfs (root file system),在bootfs之上。包含的就是典型 Linux 系统中的 /dev,/proc,/bin,/etc等标准目录和文件。rootfs就是各种不同的操作系统发行版，比如Ubuntu，Centos等等。
![Alt text](image-3.png)
对于一个精简的OS,rootfs可以很小,只需要包含最基本的命令,工具和程序库就可以了,因为底层直接用Host的kernel,自己只需要提供rootfs就可以了.由此可见对于不同的linux发行版,bootfs基本是一致的
## 分层理解
当下载一个镜像的时候,通过下载时的日志输出可以看到是一层一层的在下载.
由下图可以看到,当下载一个镜像时,这里下载了六层,其中第一层已经存在了就过滤,然后会只下载后面的五层.
 ![Alt text](image-4.png)
所有的Docker镜像都起始于一个基础镜像层,当进行修改或添加新的内容时,就会在当前镜像层之上,创建新的镜像层.
Docker镜像都是只读的,当容器启动时,一个新的可写层被加载到镜像的顶部,这一层是叫容器层.
# Commit
commit的作用举例:
例如之前部署的tomcat镜像,默认的tomcat的webapps文件夹下没有文件,将webapps.dist中的文件复制到webapps文件夹后才能正常使用.因此可以将经过修改的tomcat进行commit来创建一个属于自己的镜像.
```shell
docker commit # 提交容器成为一个新的镜像
# 命令和git原理类似
docker commit -m="提交的描述信息" -a="作者" 容器id 目标镜像名:[版本号]
```
# 容器数据卷
数据都在容器中,如果容器删除那么数据也会跟着丢失.需要将数据持久化,所以有了容器数据卷这个技术,将Docker容器中产生的数据同步到本地,将容器内的目录挂载到linux上面.还有一个好处就是其他容器也都能访问到这个本地的地址.
```shell
# 创建一个容器并且设置容器数据卷
docker run -it -v 主机目录:容器目录 镜像名字 /bin/bash
# 查看容器是否挂载
docker inspect 容器id # 查看容器元数据,查看其中是否有Mounts
```
## 部署MySQL并实现数据挂载
```shell
# -d 后台启动
# -p 端口映射
# -v 卷挂载
# -e 环境配置,这里是设置mysql的密码
# --name 容器别名
docker run -d -p 3310:3306 -v /home/mysql:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql
```
创建好名字叫mysql01的容器之后,通过DBeaver与数据库进行连接.
![Alt text](image-5.png)
## 具名挂载和匿名挂载
```shell
# 匿名挂载:当使用docker run 的-v时不指定主机内路径
docker run -d -P --name nginx01 -v /etc/nginx nginx
# 查看所有的卷的情况
docker volume ls
# 输出的像这种的都属于匿名挂载:local     04e6ed9f31af8dc6768989d7d1c8db41d5ff61400a6d28d673db9aff5d2b396d

# 具名挂载:-v时使用卷名:容器路径 而不是 主机路径:容器路径
docker run -d -P --name nginx02 -v juming-nginx:/etc/nginx nginx

# 所有的docker容器内的卷,没有指定目录的情况下都是再 '/var/lib/docker/volumes/卷名/_data下'
# 通过具名挂载可以方便的找到我们的一个卷,大多数情况在使用具名挂载  

# 总结:
-v 容器内路径 # 匿名挂载
-v 卷名:容器内路径 # 具名挂载
-v /宿主机路径:容器内路径 # 指定路径挂载

```
扩展:
```shell
# 通过 -v 容器内路径: ro rw 改变读写权限
ro :readonly
rw :readwrite 

docker run -d -P --name nginx02 -v juming-nginx:/etc/nginx:ro nginx
docker run -d -P --name nginx02 -v juming-nginx:/etc/nginx:rw nginx

# ro 意思是说明这个路径只能通过宿主机来操作,容器内部是无法操作的.
```

## 初识Dockerfile
Dockerfile就是用来构建docker镜像的构建文件
```shell
# 去home目录下创建一个docker=test-volume文件夹并创建一个dockerfile文件
cd /home
mkdir docker-test-volume
vim dockerfile1
# 进入vim编辑文本按i进入写入操作
FROM centos # 镜像名

VOLUME ["volume01","volume02"] # 挂载卷,这里是匿名挂载两个

CMD echo"----end-----" # 命令,打印
CMD /bin/bash # 进入命令行操作模式
# 写完以后按esc然后:wq完成写入保存与退出

# 通过dockerfile构建镜像
# -f 是指dockerfile文件的路径, -t 内容填 镜像名:镜像版本号 最后填个"."意思是在当前目录下生成镜像
docker build -f dockerfile1 -t mycentos:1.0 .

# 查看所有镜像,查看自己构建的镜像是否成功
docker images

# 通过自己的镜像创建容器
docker run -it mycentos:1.0 /bin/bash

# 查看通过镜像构建的容器里是否执行了dockfile文件中的命令,通过ls -l 可以发现随着创建容器的同时实现了挂载volume01和volume02
ls -l
```
 
 ## 数据卷容器
 数据卷容器:可以让一个容器专门用来管理volume,然后其他需要使用这个volume的容器就通过--volumes-from 容器名,来访问volume.
 也就是说,多个容器之间可以共享volume.
 ```shell
 # 创建一个容器,这个容器可以共享另一个容器挂载的volume
 docker run -it --volumes-from 有挂载volume的容器名 镜像名
 ```

# DockerFile
dockerfile是用来构建docker镜像的文件,命令参数脚本
构建步骤:
1. 编写一个dockerfile文件
2. docker build 构建成为一个镜像
3. docker run 运行镜像
4. docker push 发布镜像(DockerHub)

## DockerFile的构建过程
基础知识:
1. 每个保留关键字(指令)都是必须是大写字母
2. 执行从上到下顺序执行
3. #表示注释
4. 每一个指令都会创建提交一个新的镜像层并提交.
![Alt text](image-6.png)
5. dockerfile是面向开发的,以后要发布项目,做镜像,就需要编写dockerfile文件,这个文件十分简单.

## DockerFile的指令
```shell
FROM                   # 基础镜像
MAINTAINER             # 镜像是谁写的,姓名＋邮箱
RUN                    # 镜像构建的时候需要运行的命令
ADD                    # 除基础镜像外额外添加的镜像内容
WORKDIR                # 镜像的工作目录,也就是说通过镜像创建容器后进入的目录
VOLUME                 # 挂载的目录
EXPOSE                 # 暴露的端口
CMD                    # 通过镜像创建容器时执行的命令,如果创建容器的同时指定了命令则CMD不生效
ENTRYPOINT             # 通过镜像创建容器时执行的命令,如果创建容器的同时指定了命令,ENTRYPOINT仍然生效
ONBUILD                # ONBUILD中的内容只有当被FROM时才会执行,其他时候不会执行,ONBUILD指令对应的内容是其他指令以及内容.
COPY                   # 类似ADD,将文件拷贝到镜像中
ENV                    # 构建的时候设置环境变量
```

## 测试:构建自己的centos镜像
```shell
# 前往/home目录创建一个my_dockerfiles目录,然后通过vim创建一个my_dockerfile_centos文件并写内容
cd /home
mkdir my_dockerfiles
vim my_dockerfile_centos
# 写dockerfile内容:
FROM centos:7   # 之所以使用centos:7是因为centos最新版默认不支持网络不能直接使用yum -y install vim来进行安装了.
MAINTAINER ruichen<1505291171@qq.com>

ENV MYPATH /usr/local
WORKDIR $MYPATH

RUN yum -y install vim
RUN yum -y install net-tools

EXPOSE 80

CMD echo $MYPATH
CMD echo "-----end-----"
CMD /bin/bash

# 写完内容以后构建镜像文件:-f意思是dockerfile文件的路径,我这里是相对路径直接填写名字也行,-t的意思是生成的镜像的镜像名和版本号
docker -f my_dockerfile_centos -t mycentos:1.0 .

# 查看镜像的构建信息
docker history 镜像id
# 以自己构建的centos镜像举例,内容如下:
IMAGE          CREATED          CREATED BY                                       SIZE      COMMENT
f6ed0ba1956f   10 minutes ago   CMD ["/bin/sh" "-c" "/bin/bash"]                 0B        buildkit.dockerfile.v0
<missing>      10 minutes ago   CMD ["/bin/sh" "-c" "echo \"-----end-----\""]    0B        buildkit.dockerfile.v0
<missing>      10 minutes ago   CMD ["/bin/sh" "-c" "echo $MYPATH"]              0B        buildkit.dockerfile.v0
<missing>      10 minutes ago   EXPOSE map[80/tcp:{}]                            0B        buildkit.dockerfile.v0
<missing>      10 minutes ago   RUN /bin/sh -c yum -y install net-tools # bu…   198MB     buildkit.dockerfile.v0
<missing>      10 minutes ago   RUN /bin/sh -c yum -y install vim # buildkit     285MB     buildkit.dockerfile.v0
<missing>      12 minutes ago   WORKDIR /usr/local                               0B        buildkit.dockerfile.v0
<missing>      12 minutes ago   ENV MYPATH=/usr/local                            0B        buildkit.dockerfile.v0
<missing>      12 minutes ago   MAINTAINER ruichen<1505291171@qq.com>            0B        buildkit.dockerfile.v0
<missing>      2 years ago      /bin/sh -c #(nop)  CMD ["/bin/bash"]             0B        
<missing>      2 years ago      /bin/sh -c #(nop)  LABEL org.label-schema.sc…   0B        
<missing>      2 years ago      /bin/sh -c #(nop) ADD file:b3ebbe8bd304723d4…   204MB 
```
## 测试:Dockerfile制作tomcat镜像
前提:
需要准备两个压缩包
1.[apache-tomcat-9.0.22.tar.gz](https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.22/bin/apache-tomcat-9.0.22.tar.gz)
2.[jdk-8u11-linux-x64.tar.gz](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html#license-lightbox)
我是在windows上面下载的,因为本地有WinSCP这个远程传输文件的软件就直接用这个传到linux虚拟机上面的home目录下新建的文件夹上了,下载xshell的网站软件旁边有个叫Xftp 7的也可以用来传输文件
```shell
# 在自定义的目录下编写Dockerfile文件,命名dockerfile文件为"Dockerfile"好处是在build的时候会自动寻找这个名字叫"Dockerfile"的文件,就不需要-f来指定了.
mkdir /home/my_tomcat
touch readme.txt
vim Dockerfile
# Dockerfile内容:
FROM centos:7
MAINTAINER ruichen<1505291171@qq.com>

COPY readme.txt /usr/local/readme.txt

ADD jdk-8u11-linux-x64.tar.gz /usr/local/
ADD apache-tomcat-9.0.22.tar.gz /usr/local/

RUN yum -y install vim

ENV MYPATH /usr/local
WORKDIR $MYPATH

ENV JAVA_HOME /usr/local/jdk1.8.0_11
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
ENV CATALINA_HOME /usr/local/apache-tomcat-9.0.22
ENV CATALINA_BASH /usr/local/apache-tomcat-9.0.22
ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/lib:$CATALINA_HOME/bin

EXPOSE 8080

CMD /usr/local/apache-tomcat-9.0.22/bin/startup.sh && tail -f /usr/local/apache-tomcat-9.0.22/logs/catalina.out

# 构建镜像: 
docker build -t my_tomcat .
# 创建容器
docker run -d -p 9090:8080 --name mytomcat_container -v /home/my_tomcat/test:/usr/local/apache-tomcat-9.0.22/webapps/test -v /home/my_tomcat/tomcatlogs/:/usr/local/apache-tomcat-9.0.22/logs my_tomcat
# 进入容器
docker exec -it 容器id /bin/bash
# ctrl+p+q退出容器,访问域名
curl localhost:9090
# 没问题后,那么在浏览器上输入主机名然后:9090即可进入tomcat

# 发布项目(由于做了卷挂载,直接在本地编写项目就可以发布了)
# 在本地进入my_tomcat的test目录(这个test目录是挂载的目录)
cd test
# 创建一个WEB_INF目录并进入
mkdir WEB_INF
cd WEB_INF
# 写一个web.xml
vim web.xml
# 内容:
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <welcome-file-list>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>

</web-app>

# 再去test目录写一个index.jsp
cd ..
vim index.jsp
# 内容:
<%@ page language="java" contentType="text/html; charset=UTF-8"%>
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Welcome to My Website</title>
</head>
<body>
    <h1>Hello, this is the index.jsp page!</h1>
    <p>Current time: <%= new java.util.Date() %></p>
</body>
</html>
# 内容写好以后,当前浏览器地址是主机号:9090,接下来输入/test回车,也就是主机号:9090/test,回车后如果跳转网页正常跳转并显示即可证明成功

```

# Docker网络
ens33的话就是虚拟机的地址
![Alt text](image-7.png)
两个容器通过Docker0可以进行连接
<font color=red>注:如果这两个容器如果没有进行link,那么不可以直接通过容器名进行ping通,需要一个容器名对应ip地址才行</font>
![Alt text](image-8.png)
所有容器不指定网络的情况下,都是docker0路由的,docker会给容器分配一个默认的可用IP
![Alt text](image-9.png)

```shell
# 下载tomcat镜像并创建容器
docker run -d -P --name tomcat01 tomcat
# 查看容器内部网络地址
docker exec -it tomcat01 ip addr
# 查看到以后,使用ping 网络地址 的命令,发现linux可以ping通容器内部
# 每启动一个docker容器,docker就会给docker容器分配一个ip,我们只要安装了docker,就会有一个网关docker0
# 桥接模式,使用的技术是veth-pair技术
# veth-pair充当一个桥梁,连接各种虚拟设备.
# 容器与容器之间是可以互相ping通的
```
# 自定义网络
通过自定义网络可以实现容器互联,可以令不同的集群使用不同的网络,保证集群是安全和健康的.
查看所有docker网络:
docker network ls
![Alt text](image-10.png)
网络模式:
bridge: 桥接 docker默认
none : 不配置网络
host: 和宿主机共享网络
container: 容器网络联通(用的少,局限很大)
测试:
```shell
# 使用docker run -d -P --name tomcat01 tomcat命令是会有个默认参数 --net bridge也就是docker0 
# docker0特点: 默认,域名不能访问
docker run -d -P --name tomcat01 --net bridge tomcat
# 自定义网络: 网络模式为桥接模式,子网为192.168.0.0/16(这里的16意思是指开头的16个二进制数字固定),网关为192.168.0.1
docker network create --driver bridge --subnet 192.168.0.0/16 --gateway 192.168.0.1 mynet
# 通过自己的自定义网络创建两个容器
docker run -d -P --name tomcat-net-01 --net 自定义网络名字 tomcat
docker run -d -P --name tomcat-net-02 --net 自定义网络名字 tomcat
# 令通过自定义网络创建的容器01去ping通过自定义网络创建的容器02是成功的
docker exec -it 容器01 ping 容器02
```
# 网络联通
举例,这里使用默认网关创建两个容器tomcat-01与tomcat-02,使用自定义网络创建两个容器tomcat-net-01与tomcat-net-02,如果想要让tomcat-01与tomcat-net-01之间相互访问是需要先将tomcat-01与mynet网关进行联通的
![Alt text](image-11.png)
创建redis集群命令的解释:
![Alt text](image-13.png)
```shell
# 让mynet网关与tomcat01容器进行连通,将tomcat01放到了mynet网络下,一个容器两个ip地址
docker network connect mynet tomcat01
```
# 部署Redis集群
部署一个这样的集群:当r-m死掉的话,会有对应的r-s去进行替代
![Alt text](image-12.png)
```shell
# 清理所有容器
docker rm -f &(docker ps -aq)
# 创建名字叫做redis的自定义网络
docker network create redis --subnet 172.38.0.0/16
# 通过脚本创建6个redis配置
for port in $(seq 1 6); \
do \
mkdir -p /mydata/redis/node-${port}/conf
touch /mydata/redis/node-${port}/conf/redis.conf
cat << EOF >/mydata/redis/node-${port}/conf/redis.conf
port 6379 
bind 0.0.0.0
cluster-enabled yes 
cluster-config-file nodes.conf
cluster-node-timeout 5000
cluster-announce-ip 172.38.0.1${port}
cluster-announce-port 6379
cluster-announce-bus-port 16379
appendonly yes
EOF
done
# cd到/mydata查看redis是否创建出来
cd /mydata/
ls
# 启动redis-1服务
docker run -p 6371:6379 -p 16371:16379 --name redis-1 \
-v /mydata/redis/node-1/data:/data \
-v /mydata/redis/node-1/conf/redis.conf:/etc/redis/redis.conf \
-d --net redis --ip 172.38.0.11 redis:5.0.9-alpine3.11 redis-server /etc/redis/redis.conf
# 启动redis-2服务,仿照redis-1,修改端口号,容器名,映射,ip
docker run -p 6372:6379 -p 16372:16379 --name redis-2 \
-v /mydata/redis/node-2/data:/data \
-v /mydata/redis/node-2/conf/redis.conf:/etc/redis/redis.conf \
-d --net redis --ip 172.38.0.12 redis:5.0.9-alpine3.11 redis-server /etc/redis/redis.conf
# 依次顺序启动redis-3,4,5,6服务
...
# 进入redis-1容器,redis容器只能使用sh解释器
docker exec -it redis-1 /bin/sh
# 创建一个Redis集群
redis-cli --cluster create 172.38.0.11:6379 172.38.0.12:6379 172.38.0.13:6379 172.38.0.14:6379 172.38.0.15:6379 172.38.0.16:6379 --cluster-repli
cas 1
# 连接到redis集群模式
redis-cli -c
# 获取redis集群状态信息
cluster info
# 获取集群所有系欸但的详细信息
cluster nodes
# 设置键值对,a关联b,系统会自动分配一个主机器来进行这个配置,我这里显示的是ip为172.38.0.13的节点
set a b
# ctrl+p+q退出容器,停掉redis-3
docker stop redis-3
# 进入集群,去获取a
docker exec -it redis-1 /bin/sh
redis-cli -c
get a
# 最终可以看到返回结果是从14ip的节点中找到了b
# 检查所有节点,从返回中可以发现,13节点故障,14节点变成了主节点
cluster nodes
```
