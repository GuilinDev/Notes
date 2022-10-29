## Docker15个常见的问题和坑

### 1. 什么是Docker？
* Docker是一个开源的app容器引擎，基于go语言开发，并遵循apache2.0协议开源
* Docker实在Linux容器里运行app的开源工具，一种轻量级的"VM"
* Docker的容器技术可以在一台主机上轻松为任何app创建一个轻量级，可移植的，自给自足的容器

> Docker的Logo是一个蓝色鲸鱼，拖着许多集装箱，鲸鱼可以看作为宿主机host，集装箱可以理解为相互隔离的容器，每个集装箱/r容器中都包含自己的应用程序。

### 2. Docker的应用场景有哪些？
* Web应用的自动化打包盒发布
* 自动化测试和CICD
* 在服务型环境中部署和调整数据库或其他后台应用
* 从头编译或扩展现有的OpenShift或Cloud Foundry平台来搭建自己的PaaS环境

> Docker作为内部开发环境的场景： 在容器技术出现之前，公司往往通过为每个开发人员提供一台或多台VM来充当Dev/Test环境。Dev/Test环境一般负载较低，大量的系统资源都被浪费在VM本身的进程上了。

> Docker容器没有任何CPU和Memory上的额外开销，很适合用来提供公司内部的Dev/Test环境。而且由于Docker镜像可以很方便的在公司内部分享，这对Dev/Test环境的规范性很有帮助。

> 如果把容器作为Dev机使用，需要解决的是远程登录容器和容器内进程管理的问题。虽然docker的初衷是为了“微服务”架构，根据实际经验，在docker内运行多个程序，或者sshd或upstart也是可行的。

### 3. Docker优点有哪些？
* 灵活：即使最复杂的app也可以容器/集装箱化
* 轻量级：容器利用和共享主机内核
* 可互换：可以即时部署更新和升级
* 便携式：可以在本地构建成image，然后部署到云，并在任何地方运行image产生的container
* 可扩展：可以增加并自动分发容器副本
* 可堆叠：可以垂直和即时堆叠服务

![Docker Commands Diagram](../images/docker_commands_diagram.png)

> Docker是一个用于开发，交付和运行app的开放平台。Docker能够将app与基础架构分开，从而快速交付软件。Docker还可以与管理app程序相同的方式来管理基础架构。通过利用Docker的方法来快速交付，测试和部署代码，可以大大减少便携代码和在Production环境中运行代码之间的延迟。

### 4. Docker与VM之间的区别？
虚拟机通过添加Hypervisor层（虚拟化中间层），虚拟出网卡/内存/CPU等虚拟硬件，再在这之上建立虚拟机，每个虚拟机都有自己的虚拟出来的系统内核。Docker容器则是通过隔离（namespace）的方式，将file systems，进程，设备，网络等资源进行隔离，再对权限，CPU资源等进行控制（cgroup），最终让容器之间互不影响，容器无法影响宿主机host。

与VM相比，容器资源损耗要少。同样的host下，能够建立容器的数量比VM更多。

但是，VM虚拟机的安全性比容器稍好，而docker容器与host共享内核core，file system等资源，更有可能对其他容器，宿主机产生影响。

![Docker Commands Diagram](../images/VM_vs_Container_0.jpg)

| 特性      | 容器 | 虚拟机 |
| ----------- | ----------- | ----------- |
| 启动      | 秒级       | 分钟级       |
| 硬盘使用   | 一般为MB        | 一般为GB        |
| 性能   | 接近原生        | 弱于原生       |
| 系统支持量   | 单机支持上千个容器        | 单机最多支持几十个        |

### 5. Docker的三大核心
* 镜像image - Docker的镜像是创建容器的基础类似虚拟机的快照，可以理解为一个面向Docker容器引擎的只读模板。通过镜像启动一个容器，一个镜像是一个可执行的包，其中包括运行app所需要的所有内容包含代码，运行时间，库，环境变量和配置文件。Docker镜像也是一个压缩包，只是这个压缩包不只是可执行文件和环境部署脚本，还包含了完成的OS。因为大部分镜像都是基于某个OS来构建，所以很轻松的就可以构建local和remote一样的化境，这也是Docker的镜像的精髓。
* 容器container - Docker的容器是从镜像创建的运行实例，它可以被启动，停止和删除。每一个容器都是相互隔离，互不可见，以保持平台的安全性。可以把容器看作是一个简易版的Linux环境（包括了root用户权限，镜像空间，用户空间和网络空间等）和运行在其中的apps。
* 仓库Repo - 仓库注册服务器上往往存放着多个仓库，每个仓库中包含了多个镜像，每个镜像有不同的标签tag。 仓库分为public公开仓库和private私有参股。最大的public仓库是Docker Hub：https://hub.docker.com，存放了数量庞大的镜像供用户下载。

### 6. 快速安装Docker
以Red Hat/CentOS为例

```shell
yum install -y yum-utils device-mapper-persistent-data lvm2
sudo yum-config-manager
–add-repo
https://download.docker.com/linux/centos/docker-ce.repo
[root@centos7 ~] yum -y install docker-ce docker-ce-cli containerd.io
[root@centos7 ~]# docker ps --查看docker
```
```shell
[root@centos7 ~]# systemctl enable docker
[root@centos7 ~]# systemctl start docker
[root@centos7 ~]# systemctl status docker
[root@centos7 ~]# docker ps --查看容器
[root@centos7 ~]# docker version --查看版本
[root@centos7 ~]# docker info --查看版本
```

### 7. 修改Docker的存储位置

默认情况下Docker的存放位置是 
```console
/var/lib/docker
```

通过命令查看具体的存储位置
```console
docker info | grep “Docker Root Dir”
```

**修改存储到其他位置**

首先停掉docker服务
```console
systemctl stop docker
```

然后移动/var/lib/docker到目的路径
```console
mkdir -p /root/data/docker
mv /var/lib/docker /root/data/docker
ln -s /root/data/docker /var/lib/docker --快捷方式
```

