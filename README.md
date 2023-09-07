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

