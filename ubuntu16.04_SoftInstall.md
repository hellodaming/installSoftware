# Ubuntu16.04安装各种常用软件
-----
### Atom
``` shell
sudo add-apt-repository ppa:webupd8team/atom  
sudo apt-get update  
sudo apt-get install atom
```
参考来源： http://blog.csdn.net/q1302182594/article/details/51304401

-----
### Electronic WeChat
微信linux替代版

github地址： https://github.com/geeeeeeeeek/electronic-wechat

-----
### Java JDK 8

安装依赖包：
``` shell
sudo apt-get install python-software-properties
```
添加仓库源：
``` shell
sudo add-apt-repository ppa:webupd8team/java
```
更新软件包列表
``` shell
sudo apt-get update
```
安装Java JDK
``` shell
sudo apt-get install oracle-java8-installer
```

安装过程中需要接受协议，如下图所示：

![file-list](/ubuntu16.04_SoftInstall/java8Install.png)

查看是否安装完成：
``` shell
java -version
```
若能输出java8版本，则安装完成。

参考来源： http://topspeedsnail.com/ubuntu16-install-java-jdk/

-----
### 翻墙 shadowsock-Q5 + chrome插件SwitchyOmega  一顿操作安装完，忘记了具体的流程了……仅供参考

参考来源： https://github.com/shadowsocks/shadowsocks-qt5/wiki/%E5%AE%89%E8%A3%85%E6%8C%87%E5%8D%97
参考来源： https://github.com/FelisCatus/SwitchyOmega/wiki/GFWList


### steam
``` shell
sudo add-apt-repository multiverse
sudo apt update
sudo apt install steam
```
第一个是增加对第三方非自由软件库的支持，就是说系统支持第三方非自由软件；第二个命令更新软件包，第三个大家应该都知道是安装steam。其实这篇文章的中心解决方案就是打开对第三方软件的支持。


![file-list](/ubuntu16.04_SoftInstall/Steam_fatal-error.png)

参考来源： http://lib.csdn.net/article/vr/40876
参考来源： http://blog.moeoj.net/2016/07/31/%E5%9C%A8Linux%E4%B8%8B%E8%BF%90%E8%A1%8CSteam%E6%97%B6%EF%BC%8C%E6%8F%90%E7%A4%BA%E2%80%9C%E5%8A%A0%E8%BD%BDsteamui-so%E5%A4%B1%E8%B4%A5%E2%80%9D%E7%9A%84%E8%A7%A3%E5%86%B3%E6%96%B9%E6%B3%95/


### virtualbox
一开始，我在官网下载了本ubuntu16.04对应的deb包，
![file-list](/ubuntu16.04_SoftInstall/virtualbox官网.png)
并安装，一切看起来都很正常，
但是，当我启动virtualbox后，加载一个虚拟机时，它告诉我错误，并叫我用root权限执行/sbin/vboxconfig，
执行后，继续报错：
![file-list](/ubuntu16.04_SoftInstall/virtualbox_vboxconfig.png)
查资料，并各种折腾还是没有绕过这个错误。
后来，看到网上说的，用apt-get install virtualbox，而不是apt-get install virtualbox-5.1安装。
![file-list](/ubuntu16.04_SoftInstall/virtualbox_apt.png)
并执行了
apt-get install virtualbox-dkms
modprobe vboxdrv

发现最后安装的是 5.0.24版
![file-list](/ubuntu16.04_SoftInstall/virtualbox5.0.png)

加载虚拟机，发现报了不一样的错误，Could not insert 'vboxdrv'
![file-list](/ubuntu16.04_SoftInstall/virtualbox_vboxdrv.png)
有点开心，毕竟发生了不同的错误了……
上网查之，尝试之，网上有人说(链接：http://askubuntu.com/questions/760671/could-not-load-vboxdrv-after-upgrade-to-ubuntu-16-04-and-i-want-to-keep-secur)是boot的secure Boot的原因，disable之，
![file-list](/ubuntu16.04_SoftInstall/virtualbox_secure.jpg)
发现可以安装了！！！安装win10，ok
![file-list](/ubuntu16.04_SoftInstall/vitualbox_ok.png)

安装virtuabox扩张包。
找到相应的包https://www.virtualbox.org/wiki/Download_Old_Builds_5_0
管理->全局设定->扩展；找到下载好的包，安装之
![file-list](/ubuntu16.04_SoftInstall/virtualbox_extend.png)


发现安装好的win10的无缝模式无法开启，
故而安装增强功能（设备->安装增强功能）
![file-list](/ubuntu16.04_SoftInstall/virtualbox_增强功能.png)
进入win10虚拟机后，通过镜像进行安装
![file-list](/ubuntu16.04_SoftInstall/virtualbox_增强功能2.png)
![file-list](/ubuntu16.04_SoftInstall/virtualbox_增强功能3.png)

ok！
用了差不多1天时间折腾这个，我晕
 at 2016/09/19

### vim C++ 各种折腾还是失败了……
https://github.com/VundleVim/Vundle.vim/blob/master/README_ZH_CN.md

http://howiefh.github.io/2015/05/22/vim-install-youcompleteme-plugin/
sudo apt-get install build-essential cmake
