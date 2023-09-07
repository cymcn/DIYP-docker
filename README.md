# VM虚拟机-安装OPENWRT
账号：root  
密码：password

如何在vmware虚拟机中安装OpenWrt系统: https://segmentfault.com/a/1190000024463689

                                    https://zhuanlan.zhihu.com/p/334419721
                                    
                                    https://www.jb51.net/article/241586.htm
                                    

查看IP:ifconfig

开机进入系统后输入如下命令配置网络：vi /etc/config/network

按i键进入编辑状态，修改 option ipaddr 里面的IP地址（应设置为当前同一局域网段之内，比如目前路由器的IP地址是192.168.1.1，OpenWrt/LEDE的IP地址可设置为192.168.1.200）,

按esc键退出，输入:wq保存退出

保存之后重启网卡或者重启虚拟机

重启网络命令：service network restart

重启虚拟机命令：reboot


# docker

 ## 卸载 Docker：
停止所有正在运行的 Docker 容器。可以使用以下命令停止所有容器:

docker stop $(docker ps -aq)

删除所有的 Docker 容器。可以使用以下命令删除所有容器：

docker rm $(docker ps -aq)

删除所有的 Docker 镜像。可以使用以下命令删除所有镜像：

docker rmi $(docker images -aq)

删除 Docker 的数据目录。默认情况下，Docker 的数据目录位于 /var/lib/docker。您可以使用以下命令删除该目录：

sudo rm -rf /var/lib/docker


## Docker删除 容器：
首先，使用以下命令列出正在运行的 Docker 容器：

docker ps

这将显示正在运行的容器的列表，包括容器的名称或 ID。

找到您想要卸载的容器，并记下其名称或 ID。

使用以下命令停止该容器：

docker stop <容器名称或 ID>

将 <容器名称或 ID> 替换为您要停止的容器的名称或 ID。

使用以下命令删除该容器：

docker rm <容器名称或 ID>

将 <容器名称或 ID> 替换为您要删除的容器的名称或 ID。

## Docker删除 镜像：

首先，使用以下命令列出所有的 

docker images

这将显示已安装的镜像列表，包括镜像的名称和标签。

找到您想要删除的镜像，并记下其名称和标签。

使用以下命令删除该镜像：

docker rmi <镜像名称:标签>

将 <镜像名称:标签> 替换为您要删除的镜像的名称和标签。如果镜像没有标签，可以省略 :标签。

## openwrt 安装docker:
           https://juejin.cn/s/openwrt%20%E5%AE%89%E8%A3%85docker
 确保您的 OpenWrt 路由器已经连接到互联网，并且已经安装了 opkg 包管理工具。如果您尚未安装 opkg，请执行以下命令进行安装：
 
opkg update
opkg install opkg

安装 Docker 包。在终端中运行以下命令：

opkg update
opkg install docker

启动 Docker 服务。在终端中运行以下命令：

/etc/init.d/docker start

现在，您已经成功在 OpenWrt 上安装并启动了 Docker。您可以使用以下命令检查 Docker 是否已经成功运行：

docker info

如果 Docker 正确运行，则会显示 Docker 的一些基本信息。

