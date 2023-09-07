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




#  docker部署项目

## 1.官方PHP8.2 Docker一键命令：
 安装 Docker
opkg update
opkg install docker

 启动 Docker 服务
/etc/init.d/docker start

 拉取 PHP 8.2.x 镜像并运行容器（5211是可调整端口）
docker run -d -p 5211:80 --name php-container php:8.2 php -S 0.0.0.0:80 -t /var/www/html

在根目录 root/root建test文件夹，
把***.php文件上传到/root/root/test
TTYD终端命令：
           docker cp /root/test/***.php php-container:/var/www/html/


访问地址：
http://你的IP:5211/xxx.php?id=xxx&xx=xxx...
               如：/huya.php?id=11342387
                  /douyu.php?id=4246519

## 2.肥羊的项目：
Docker仓库地址：https://hub.docker.com/repositories/youshandefeiyang
GitHub仓库地址：https://github.com/youshandefeiyang

PHP集成肥羊解密扩展环境Docker镜像（基于PHP8.1）：
本镜像既可以运行普通PHP程序，又可以运行肥羊加密PHP代理，使用方法：
一键运行：

amd64架构：
docker run -d --restart unless-stopped --privileged=true -p 5678:80 --name php-env youshandefeiyang/php-env


（docker run: 这是运行 Docker 容器的命令。
-d: 这个参数表示以后台（detached）模式运行容器，使其在后台运行而不阻塞终端。
--restart unless-stopped: 这个参数指定了容器的重启策略，除非手动停止容器，否则容器会在退出或重启时自动重启。
--privileged=true: 这个参数赋予容器特权，允许容器内的进程拥有访问主机系统的权限。
-p 5678:80: 这个参数将主机的端口 5678 映射到容器的端口 80，这样可以通过访问主机的 5678 端口来访问容器中运行的应用程序。
--name php-env: 这个参数为容器指定一个名称，即 "php-env"。
youshandefeiyang/php-env: 这是要拉取的 PHP 环境镜像的名称。Docker 会从 Docker Hub 上下载该镜像，以便在容器中运行 PHP 环境）

arm64架构：
docker run -d --restart unless-stopped --privileged=true -p 5678:80 --name php-env youshandefeiyang/php-env:arm64

然后执行：
docker cp /root/test/xxx.php php-env:/var/www/html/

访问地址：
http://你的IP:5678/xxx.php?id=xxx&xx=xxx.

## 3.青龙面版：
https://www.right.com.cn/forum/thread-6579104-1-1.html

 青龙v2.12.0及以上版本安装命令：
docker run -dit \
-v $PWD/ql:/ql/data \
-v $PWD/ql/ninja:/ql/data/ninja \
-v $PWD/ql/xdd:/ql/data/xdd \
-v $PWD/ql/xdd-plus:/ql/data/xdd-plus \
-v $PWD/ql/sillyGirl:/ql/data/sillyGirl \
-p 5700:5700 \
-p 5701:5701 \
-e ENABLE_HANGUP=true \
-e ENABLE_WEB_PANEL=true \
-e ENABLE_TG_BOT=true \
--name qinglong \
--hostname qinglong \
--restart unless-stopped \
whyour/qinglong:latest


青龙v2.11.3及以下版本安装命令：
docker run -dit \
-v $PWD/ql/config:/ql/config \
-v $PWD/ql/scripts:/ql/scripts \
-v $PWD/ql/repo:/ql/repo \
-v $PWD/ql/log:/ql/log \
-v $PWD/ql/db:/ql/db \
-v $PWD/ql/deps:/ql/deps \
-v $PWD/ql/jbot:/ql/jbot \
-v $PWD/ql/raw:/ql/raw \
-v $PWD/ql/ninja:/ql/ninja \
-v $PWD/ql/xdd:/ql/xdd \
-v $PWD/ql/xdd-plus:/ql/xdd-plus \
-v $PWD/ql/sillyGirl:/ql/sillyGirl \
-p 5700:5700 \
-p 5701:5701 \
-e ENABLE_HANGUP=true \
-e ENABLE_WEB_PANEL=true \
-e ENABLE_TG_BOT=true \
--name qinglong \
--hostname qinglong \
--restart unless-stopped \
whyour/qinglong:2.11.3




# ZY Player （电脑版tvbox）
接口（自用-简单）：https://ghproxy.com/https://raw.githubusercontent.com/cymcn/ZyPlayer-.json/main/123.json
                 （https://url.480583.xyz/zp11）
接口：（自用-全面）https://ghproxy.com/https://raw.githubusercontent.com/cymcn/myTVBox/main/sub/zp.json
                   (https://url.480583.xyz/zp22)

接口采集网址：https://www.yszzq.com/

原版：https://github.com/Hunlongyu/ZY-Player
2次开发版：https://github.com/Hiram-Wong/ZyPlayer
