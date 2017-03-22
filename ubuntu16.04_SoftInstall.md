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

今天帮同学的window时，安装增强工具各种失败：未能加载虚拟光驱 VBoxsGuestAdditions.iso到虚拟电脑
后来google一下，找到解决方法了
链接： http://zycao.com/virtualbox-ubuntu-vboxsguestadditions.html




### vim C++ 各种折腾还是失败了……
~~https://github.com/VundleVim/Vundle.vim/blob/master/README_ZH_CN.md~~

~~http://howiefh.github.io/2015/05/22/vim-install-youcompleteme-plugin/
sudo apt-get install build-essential cmake~~


20160923号的时候，重新安装一下就好了（关键是要在网络好的情况下安装YouCompleteMe，这个插件的确有点大，下载速度又太慢了）

### 有道词典
英文差，词汇量少，经常要查字典，所以安装个有道词典

去有道官网下载了相关deb包，一开始没有留意有ubuntu版本，下了deepin的版本（ youdao-dict_1.1.0-0-deepin_amd64.deb）

用dpkg安装该包。
![file-list](/ubuntu16.04_SoftInstall/youdao-dict_dpkg.png)
果断报了缺失依赖包的错误。
上网查之，利用ubuntu的apt-get，自动补全依赖包
使用
``` bash
apt-get -f -y install
```
解决依赖问题后，重新执行dpkg安装deb包，成功
![file-list](/ubuntu16.04_SoftInstall/youdao-dict_ok.png)
居然用deepin的版本也能安装。deepin果然是ubuntu的兄弟

参考来源： http://www.cnblogs.com/horizonli/p/5179224.html

### aria2c下载 + webui-aria2下载百度云资源
``` bash
sudo add-apt-repository ppa:t-tujikawa/ppa
sudo apt-get update
sudo apt-get install aria2
```
aria2c 安装好了……

添加对百度云的配置

~~创建存放配置文件的目录~~
``` bash
mkdir ～/.aria2
```

下载下面目录下的所有配置文件，
[./aria2](/ubuntu16.04_SoftInstall/.aria2)

并把./aria2这个文件放在用户目录（即： ~/）

配置./aria2目录下的aria2.conf,高亮的部分。
![file-list](/ubuntu16.04_SoftInstall/aria2_conf.png)
配置完成后，执行
``` bash
aria2c --conf-path=/XXX/aria2.conf
```
/XXX 代表aria2.conf的路径。

在https://github.com/acgotaku/BaiduExporter中下载安装chrome的BaiduExporter插件。
安装完成后，

打开百度云链接，就多出一个“导出下载”的选项。
![file-list](/ubuntu16.04_SoftInstall/aria2_download.png)
选取ARIA2 RPC，就可以进行百度网盘资源的下载了。而且好像还是没有速度限制的哦。

问题来了，我安装网上的教程，发现下载的时候登陆http://ziahamza.github.io/webui-aria2/
时，并没有下载信息的显示。

解决方法1：
点击页面的“设置” -> “连接设置”，设置“主机”为localhost；设置“端口”为6800 。 保存连接设置。
![file-list](/ubuntu16.04_SoftInstall/aria2_webui-aria2.png)
页面右上角显示：

正在尝试使用新的连接设置来连接到 Aria2

过了一会儿，就能显示出你的下载信息了。


解决方法2：
去https://github.com/ziahamza/webui-aria2
，把它clone到本地，然后打开目录下的index.html，就能显示相关下载信息了
![file-list](/ubuntu16.04_SoftInstall/aria2_download2.png)

参考资料：http://www.jianshu.com/p/d7e01982e474

参考资料：http://www.cnblogs.com/zz0412/p/3416683.html

参考资料：https://github.com/acgotaku/BaiduExporter

 参考资料：
 http://moflying.com/2016/06/05/%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8aria2%E5%8F%8Awebui-aria2%E4%B8%8B%E8%BD%BD%E7%99%BE%E5%BA%A6%E4%BA%91%E8%B5%84%E6%BA%90/



### latex + Atom
安装 Tex Live
```bash
sudo apt-get install texlive-full
```
出乎意料的大，有1900+M。

安装完不能用，
需用一个编辑器，这里我还是使用先前已经安装好的Atom。

打开Atom，左上角Edit -> Preferences , 打开Setting，点击install，搜索并安装下面三个packages：

```bash
语言高亮：language-latex
编译：latex
PDF预览：pdf-view
```

安装完成后，就能在Atom中新建文件，并在右下角选择LaTeX作为文件高亮语言

参考资料： https://xuewenyuan.github.io/2016/10/20/TexLive+Atom/   
参考资料： http://www.cnblogs.com/schaepher/p/5934184.html


### 安装 octave
```bash
sudo apt-add-repository ppa:octave/stable
sudo apt-get update
sudo apt-get install octave
```
安装后，点击octave，

出现错误：
The settings file /home/user/.config/octave/qt-settings does not exist and can not be created.
Make sure you have read and write permissions to /home/user/.config/octave
Octave GUI must be closed now.

解决方法：
```bash
cd .config/octave
sudo chown user qt-settings
```
参考资料： http://blog.topspeedsnail.com/archives/6432  
参考资料： http://unix.stackexchange.com/questions/292721/error-running-octave-in-ubuntu-16-04



### 给一台i7-6700 GTX1070 主板技嘉B150主板的电脑安装Ubuntu16.04


遇到的坑1 ： 屏幕线原来连接在PCIe1的接口上，在重启进入安装页面后，刚刚看到Ubuntu的配置页面的时候，显示屏黑了，然后显示屏闪过 类似 ……1920*1080*60 ……

的字样（当时忘记拍照了！），

解决方案：估计是因为显卡的问题，所以进主板的BIOS，把Internal Graphics(内建显示功能)，把它改成：Disabled（关闭），然后 Init Display First 由PCIe1改成IGFX，最后把显示器数据线接到电源旁边的接口，OK


遇到的坑2 ： 选用了一个USB3.1的U盘作为启动盘，但选择分区后，确定安装，几乎立马提示的错误:
```bash
This particular error is often due to a faulty CD/DVD disk or drive, or a faulty hard disk. It may help to clean the CD/DVD, to burn the CD/DVD at a lower speed, to clean the CD/DVD drive lens (cleaning kits are often available from electronics suppliers), to check whether the hard disk is old and in need of replacement, or to move the system to a cooler environment.
```
后来换了个USB2.0的U盘作为启动盘 就好了。原因未明
