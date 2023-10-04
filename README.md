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

docker ps <列出所有容器 ID>

docker stop <停止-容器ID>

docker rm <删除-容器ID>

docker images <列出所有镜像 ID>

docker rmi <镜像ID>

docker stop $(docker ps -aq)      <停止所有容器>

docker rm $(docker ps -aq)      <删除所有容器>

docker rmi $(docker images -aq)  <删除所有镜像>

sudo rm -rf /var/lib/docker   <删除该目录>

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




#  **********************  docker部署项目     **********************  
#  **********************  docker部署项目     **********************  
#  **********************  docker部署项目     **********************  
#  **********************  docker部署项目     **********************  

代码说明：

docker run -d --restart unless-stopped --privileged=true -p 5678:80 --name php-env youshandefeiyang/php-env


docker run: 这是运行 Docker 容器的命令。

-d: 这个参数表示以后台（detached）模式运行容器，使其在后台运行而不阻塞终端。

--restart unless-stopped: 这个参数指定了容器的重启策略，除非手动停止容器，否则容器会在退出或重启时自动重启。

--privileged=true: 这个参数赋予容器特权，允许容器内的进程拥有访问主机系统的权限。

-p 5678:80: 这个参数将主机的端口 5678 映射到容器的端口 80，这样可以通过访问主机的 5678 端口来访问容器中运行的应用程序。

--name php-env: 这个参数为容器指定一个名称，即 "php-env"。

youshandefeiyang/php-env: 这是要拉取的 PHP 环境镜像的名称。Docker 会从 Docker Hub 上下载该镜像，以便在容器中运行 PHP 环境）

## 1.官方PHP8.2 Docker一键命令：

拉取 PHP 8.2.x 镜像并运行容器（5211是可调整端口）：

docker run -d -p 5211:80 --restart unless-stopped --name php-container php:8.2 php -S 0.0.0.0:80 -t /var/www/html


在根目录 root/root建test文件夹

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


docker run: 这是运行 Docker 容器的命令。

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


## 3.Alist 安装：
   https://hub.docker.com/r/xhofe/alist
   https://alist.nn.ci/zh/guide/install/docker.html

 稳定版:
 
  docker run -d --restart=always -p 5244:5244 -e PUID=0 -e PGID=0 -e UMASK=022 --name="alist" xhofe/alist:latest

Docker安装怎么更新:

docker ps -a #查看容器(找Alist容器的ID)

docker stop ID #停止Alist运行,不然无法删除(这次Alist容器的ID是d429749a6e69，每一次安装都不一样自己看)

docker rm ID #删除Alist容器(数据还在只要你不手动删除)

docker pull xhofe/alist:latest

## 4.监控运行时间（uptime-kuma）:
https://github.com/louislam/uptime-kuma

docker run -d --restart=always -p 3001:3001 -v uptime-kuma:/app/data --name uptime-kuma louislam/uptime-kuma:1

## 5.ChatGPT-Next-Web:
https://github.com/Yidadaa/ChatGPT-Next-Web

docker pull yidadaa/chatgpt-next-web

docker run -d -p 3000:3000 \
   -e OPENAI_API_KEY=sk-xxxx \
   -e CODE=your-password \
   yidadaa/chatgpt-next-web
   
您可以在代理后面启动服务：

docker run -d -p 3000:3000 \
   -e OPENAI_API_KEY=sk-xxxx \
   -e CODE=your-password \
   -e PROXY_URL=http://localhost:7890 \
   yidadaa/chatgpt-next-web

## 6.自动签到（qd）:
https://github.com/qd-today/qd/

镜像：https://hub.docker.com/r/a76yyyy/qiandao

安装一键：
docker run -d -p 5278:80 --restart unless-stopped --name qiandao a76yyyy/qiandao

##  7.刮削alist聚合网盘:
https://github.com/msterzhang/onelist
https://github.com/cymcn/guaxiao-alist/blob/main/docs/docker_install.md

安装一键：
docker run -d --name onelist -e PUID=0 -e PGID=0 -e TZ=Asia/Shanghai -p 5245:5245 -v /root/onelist/config:/config --add-host api.themoviedb.org:13.224.161.90 msterzhang/onelist:latest


##  8.可道云（私有云）

代码：docker run -d -p 8001:80 --name kodexplorer -v /mnt/sdb1/kodexplorer:/var/www/html azking/kodexplorer:4.4.0

##  9.adguardhome（去广告）

代码：docker run --name adguardhome -v /opt/adguardhome/workdir:/opt/adguardhome/work -v /opt/adguardhome/confdir:/opt/adguardhome/conf -p 3001:53/tcp -p 3001:53/udp -p 3002:67/udp -p 3003:68/tcp -p 3003:68/udp -p 3004:80/tcp -p 3005:443/tcp -p 3006:853/tcp -p 3007:3000/tcp -d adguard/adguardhome

##  10.轻量级个人网盘：

    docker run \
    -v /path/to/root:/srv \
    -v /path/filebrowser.db:/database.db \
    -v /path/.filebrowser.json:/.filebrowser.json \
    -p 8080:80 \
    filebrowser/filebrowser

##  11.免费音乐播放器：

docker run -d --name music -p 264:264 -v <本机缓存目录>:/var/www/html/cache oldiy/music-player-docker

##  12.steam挂卡：

docker run -it -p 1242:1242 -v /opt/asf:/app/config --name asf justarchi/archisteamfarm

##  13.红白机怀旧游戏：

docker run -d --name dosgame -p 262:262 oldiy/dosgame-web-docker:latest

##  14.发卡系统：

docker run --name kmfaka -itd -p 8777：8000 baiyuetribe / kamifaka：latest
后台（ip:8777/admin）管理员：账号admin@qq.com 密码123456

##  15.精简版宝塔系统：

docker run -tid --name baota -p 88:80 -p 8888:8888 --restart always baiyuetribe/baota_mini #仅300mb

##  16. Docker 管理器

Portainer https://docs.portainer.io/v/ce-2.9/start/install/server/docker/linux
docker run -d -p 8000:8000 -p 9443:9443 --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    portainer/portainer-ce:latest
    
##  17. 另一个管理程序 Docker 管理器 

连接后点更多 可以选择 简体中文

docker run -d -p 10086:10086 -v /var/run/docker.sock:/var/run/docker.sock tobegit3hub/seagull

##  18. Docker快速搭建 onlyoffice开源在线办公套件

docker run -dit -p 6666:80 --restart=always onlyoffice/communityserver

##  19. 演示oneindex搭建

docker run -d -p 8181:80 --restart=always baiyuetribe/oneindex   

##  20. 人人影视

docker run -d -p 3001:3001 -v /opt/rrdata:/opt/work/store --name rrys baiyuetribe/rrshare  

##  21. 在线播放视频

docker run -t -p 10010:80 -v /opt/rrdata:/h5ai --name h5ai ilemonrain/h5ai:full  

##  22. 宝塔迷你版

docker run -tid --name baota -p 80:80 -p 8888:8888 --restart always baiyuetribe/baota_mini

##  23. zdir

mkdir /var/zdir

docker run -d -p 8080:80 -v zdir:/var/www/html/var baiyuetribe/zdir

##  24. docker搭建wireguard

https://vksec.com/2021/07/08/194_docker%E6%90%AD%E5%BB%BAwireguard/

##  25. Docker安装SaKuli桌面环境（基于Centos系统、附带chrome，支持中文）

docker run -d -p 6080:6080 -e VNC_RESOLUTION=1920x1080 wangguanzzz/xfce-desktop

##  26. Docker安装Xfce桌面环境（轻量可视化操作系统）

docker run -d -p 6080:6080 -e VNC_RESOLUTION=1920x1080 yangxuan8282/alpine-xfce4-novnc:amd64

##  27. Docker安装Raspbian（树莓派操作系统）

docker run -d -p 6080:6080 yangxuan8282/pixel-novnc:amd64

docker run -d -p 6080:6080 -v /var/run/docker.sock:/var/run/docker.sock -v /tmp/.X11-unix:/tmp/.X11-unix yangxuan8282/pixel-novnc:amd64

##  28. 百度云盘Docker版安装方法(速度比普通客户端快)

https://github.com/Baiyuetribe/baiduyunpan

##  29. Diving：一款在线分析Docker镜像的工具，可本地部署（已开源） 可以查看docker的image文件

  基于 dive 分析 docker 镜像，界面化展示了镜像每层的变动（增加、修改、删除等）、用户层数据大小等信息。便捷获取镜像信息和每层镜像内容的文件树，可以方便地浏览镜像信息。对于需要优化镜像体积时非常方便
  
  项目地址：https://github.com/vicanso/diving
  
  docker run -d --restart=always -v /var/run/docker.sock:/var/run/docker.sock -p 7001:7001 vicanso/diving

# Docker Macvlan下运行OpenWrt旁路由

 qbittorrent
 
 https://hub.docker.com/r/linuxserver/qbittorrent

# 编译固件 

  https://github.com/x-wrt
  
  直接下载固件网盘 https://drive.google.com/drive/folders/1dqNUrMf9n7i3y1aSh68U5Yf44WQ3KCuh
  
  参考文章 https://github.com/esirplayground/VPS_OpenWrt
  
  https://hub.docker.com/r/unifreq/openwrt-aarch64

# 渗透测试parrotsec环境

docker run -d -p 10022:22 -ti --name parrot -v $PWD/work:/work parrotsec/core

docker run -d -p 10022:22 -ti --name parrot -v $PWD/work:/work parrotsec

docker run -d -ti --name pdebian -v $PWD/work:/work debian




