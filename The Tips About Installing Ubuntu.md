# 安装Ubuntu16.04必看
## 1.安装VMware Tools（虚拟机）
### （1）连接CD/DVD 2
```
右键【设置】-->【硬件】-->【CD/DVD 2（SATA）】-->【设备状态】-->勾选上【已连接】和【启动时连接】<br />
                                            -->【使用ISO映像文件】-->【C:\Program Files (x86)\VMware\VMware Workstation\linux.iso】
```                                            
### （2）安装VMware Tools
#### a.在资源管理器中找到VMware Tools光盘打开
```
将VMwareTools-10.3.21-14772444.tar.gz复制到/tmp/下
解压，然后在解压后的目录下开启terminal，然后sudo ./vmware-install.pl
然后会启动安装程序
第一项的询问需要输入yes
后面自动按回车默认安装就可以了

全部安装完毕后需要reboot（重启）
```
## 2.修复Ubuntu在自动锁屏后重新登陆时无法输入密码并提示“Failed to authenticate”的bug

见https://github.com/meisa233/Working_Notes/blob/main/gnome_authentication_error_when_logging_in_after_locking.md<br />
建议选择【永久解决方案】
<br />
## 3.修复Ubuntu启动时提示SMBus Host controller not enabled的bug

https://github.com/meisa233/Working_Notes/blob/main/SMBus%20Host%20controller%20not%20enabled.md<br />

**如果有这种情况请选择修复**

## 4.更新apt源
<br />
https://github.com/meisa233/Working_Notes/blob/main/Latest_apt_sources_in_China.md<br />
升级系统包
```
sudo apt upgrade
```
如果遇到询问是否需要更新版本的提示框，请选择保持当前版本（以keep开头的选项）<br />

### 若update时遇见AppStream cache update completed, but some metadata was ignored due to errors的bug
解决方案(来源：https://www.cnblogs.com/G921123/p/10502165.html)
```
sudo rm /var/lib/dpkg/lock
sudo apt-get update
```
### 若使用apt安装包时遇见E: Could not get lock /var/lib/dpkg/lock-frontend的bug
具体bug如下提示
```
E: Could not get lock /var/lib/dpkg/lock-frontend - open (11: Resource temporarily unavailable)
E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), is another process using it?
```
解决方法：https://blog.csdn.net/shimadear/article/details/90598646<br />
#### 请按顺序执行以下的解决方案
#### a.杀死占用apt的进程
```
ps aux | grep -i apt
```
杀死相关的进程（进程号）
```
sudo kill -9 <process id>
```
或者不执行上面两条，只执行下面这一条
```
sudo killall apt apt-get 
```
#### b.杀死占用lock file的进程同时删除lock file
查询占用lock file的进程
```
lsof /var/lib/dpkg/lock
lsof /var/lib/apt/lists/lock
lsof /var/cache/apt/archives/lock
```
如果有相关进程被占用，请kill掉<br />
然后删除lock file
```
sudo rm /var/lib/apt/lists/lock
sudo rm /var/cache/apt/archives/lock
sudo rm /var/lib/dpkg/lock
```
重新配置一下dpkg
```
sudo dpkg --configure -a
```
#### c.当执行完a和b仍然会出error
可能会出现以下提示
```
dpkg: error: dpkg frontend is locked by another process
```
那么，请按照如下命令进行解决
找出正在占用lock file的进程
```
lsof /var/lib/dpkg/lock-frontend
```
杀死占用了lock file的进程（如果上面那个命令被执行后什么都没有，请忽略下面这个命令）
```
sudo kill -9 PID
```
删除lock file并重新配置dpkg
```
sudo rm /var/lib/dpkg/lock-frontend
sudo dpkg --configure -a
```
## 5.安装Unity
请务必安装，不然upgrade之后系统的任务栏很有可能会由于某些bug消失。<br />
来源：https://www.cnblogs.com/aaron-agu/p/10523032.html
```
sudo apt-get update

sudo apt-get install --reinstall ubuntu-desktop     # 如果有依赖导致安装不成功使用 aptitude install ubuntu-desktop

sudo apt-get install unity                                      # 如果有依赖导致安装不成功使用 aptitude install unity，第一种解决方案不成功选则n，使用第二种解决方案

systemctl daemon-reload

sudo service lightdm restart 重启lightdm
```
如果界面已经出问题了，并且右键也打不开terminal了，那么需要按照以下步骤修复<br />
Ctrl+Alt+F1切换到命令行界面<br />
在虚拟机中，此时系统有可能是上不了网的，需要按照以下步骤重新设置<br />
可以使用```ifconfig```命令查看是否有自己的（除了127.0.0.1）ip地址<br />
若没有，则进行修复<br />
教程来源：https://blog.csdn.net/qq_40141862/article/details/86657408<br />
```
su #切换到root用户下
   #若不知道root用户的密码，使用sudo passwd root进行修改
dhclient -v
ifconfig
```
然后需要增加DNS解析ip
```
sudo vi /etc/resolv.conf
添加
nameserver 180.76.76.76
```
保存之后即可上网<br />
```
sudo apt-get update
sudo apt-get install --reinstall ubuntu-desktop  
sudo apt-get install unity 
systemctl daemon-reload
reboot
```
