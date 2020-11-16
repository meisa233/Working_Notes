# 安装Ubuntu必看
## 1.安装VMware Tools（虚拟机）
### （1）连接CD/DVD 2
右键【设置】-->【硬件】-->【CD/DVD 2（SATA）】-->【设备状态】-->勾选上【已连接】和【启动时连接】<br />
                                            -->【使用ISO映像文件】-->【C:\Program Files (x86)\VMware\VMware Workstation\linux.iso】
### （2）安装VMware Tools
#### a.在资源管理器中找到VMware Tools光盘打开
将VMwareTools-10.3.21-14772444.tar.gz复制到**/tmp/**下<br />
解压，然后在解压后的目录下开启terminal，然后**sudo ./vmware-install.pl**<br />
然后会启动安装程序<br />
第一项的询问需要输入**yes**<br />
后面自动按回车默认安装就可以了<br />

全部安装完毕后需要reboot（重启）<br />
## 2.修复Ubuntu在自动锁屏后重新登陆时无法输入密码并提示“Failed to authenticate”的bug<br />
见https://github.com/meisa233/Working_Notes/blob/main/gnome_authentication_error_when_logging_in_after_locking.md
建议选择【永久解决方案】
## 3.修复Ubuntu启动时提示SMBus Host controller not enabled的bug<br />
https://github.com/meisa233/Working_Notes/blob/main/SMBus%20Host%20controller%20not%20enabled.md
**如果有这种情况请选择修复**
## 4.更新apt源
https://github.com/meisa233/Working_Notes/blob/main/Latest_apt_sources_in_China.md
升级系统包
```
sudo apt upgrade
```
如果遇到询问是否需要更新版本的提示框，请选择保持当前版本（以keep开头的选项）
### 若update时遇见AppStream cache update completed, but some metadata was ignored due to errors的bug
解决方案(来源：https://www.cnblogs.com/G921123/p/10502165.html)
```
sudo rm /var/lib/dpkg/lock
sudo apt-get update
```
