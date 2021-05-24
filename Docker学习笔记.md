# 简单认识一下docker
***

- **Docker Client** : Docker提供给用户的客户端。Docker Client提供给用户一个终端，用户输入Docker提供的命令来管理本地或者远程的服务器。
- **Docker Daemon** : Docker服务的守护进程。每台服务器（物理机或虚机）上只要安装了Docker的环境，基本上就跑了一个后台程序Docker Daemon，Docker Daemon会接收Docker Client发过来的指令,并对服务器的进行具体操作。
- **Docker Images** : 俗称Docker的镜像，这个可难懂了。你暂时可以认为这个就像我们要给电脑装系统用的系统CD盘，里面有操作系统的程序，并且还有一些CD盘在系统的基础上安装了必要的软件，做成的一张 **“只读”** 的CD。
- **Docker Registry** : 这个可认为是Docker Images的仓库，就像git的仓库一样，用来管理Docker镜像的，提供了Docker镜像的上传、下载和浏览等功能，并且提供安全的账号管理可以管理只有自己可见的私人image。就像git的仓库一样，docker也提供了官方的Registry，叫做Dock Hub([http://hub.Docker.com)](https://developer.aliyun.com/article/63035)
- **Docker Container** : 俗称Docker的容器，这个是最关键的东西了。Docker Container是真正跑项目程序、消耗机器资源、提供服务的地方，Docker Container通过Docker Images启动，在Docker Images的基础上运行你需要的代码。 **你可以认为Docker Container提供了系统硬件环境，然后使用了Docker Images这些制作好的系统盘，再加上你的项目代码，跑起来就可以提供服务了。** 听到这里，可能你会觉得是不是有点像一个VM利用保存的备份或者快照跑起来环境一样，其实是挺像的，但是实际上是有本质的区别，后面我会细说。

![img](http://ata2-img.cn-hangzhou.img-pub.aliyun-inc.com/5d04473994d0b4730f9d03f63f617058.png)

# docker的特点

1. docker image的体积非常的小
2. docker的系统启动的耗时为0。昨天如果自己也尝试启动hello-world的同学可能会知道，`docker run hello-world`的命令是瞬间完成的，你并没有感觉到加载image，启动系统的耗时，命令完成就直接输出了结果。程序执行完后container也跟着关闭，也并没有保存镜像的时间，但下次再运行还是会保留你处理过的状态。
3. docker系统占用资源极少，我们知道如果我们开启了一个vm的系统，不论是linux的或者windows，就算什么都不运行都会占用一部分内存，但是docker container启动后如果不运行程序，你是看不到系统资源被占用的。

我们知道VM技术可以将一台物理机器部署为多台虚拟机器，解决了很多物力资源的浪费以及方便的管理能力。那么VM是怎么做到的呢？关键词：Hypervisor，VM在物理机器的操作系统上建立了一个中间软件层Hypervisor，Hypervisor利用物理机器的资源，虚拟出多个新虚拟的硬件环境，这些硬件环境可以共享宿主机的资源。这些新的虚拟的硬件环境，安装操作系统和相应的软件后便形成了一台台的虚拟机器。

Docker选择了和虚拟化完全不同的思路，并不去虚拟化任何硬件，而是对硬件资源在不同的docker container之间做了 **“隔离”** 。隔离使每个docker container之间拥有了不同的环境（硬盘空间、网络、系统的工具包），并且又可以共享需要的硬件资源（cpu、内存、系统内核），达到了和虚拟机能提供的同样的功能。

![img](http://ata2-img.cn-hangzhou.img-pub.aliyun-inc.com/ba6d92b3ee037c9ed576f47ae5edf091.jpg)

Dcoker通过很多的所谓 **隔离** 的方式，让多个docker container之间共享了同一台机器上的资源，但又是相互隔离的（比如container1 和 container2 用的是完全不同的硬盘空间、网络地址等），这样就让docker container成为了我们项目理想的开发、测试、发布的环境。非常的轻量，简单，易于分发和管理。这也就是docker的目标:Build, Ship and Run Any App, Anywhere!
