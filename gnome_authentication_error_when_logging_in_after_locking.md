# 新安装的Ubuntu在自动锁屏后重新登陆时无法输入密码并提示“Failed to authenticate”
## 问题及解决方法来源：[askbot.fedoraproject.org](https://askbot.fedoraproject.org/en/question/115963/gnome-authentication-error-when-logging-in-after-lock/)
### 解决方案

#### 1.临时解决方案
```
sudo -i
echo 1048576 > /proc/sys/fs/inotify/max_user_watches
exit
```
#### 2.永久解决方案
```
sudo gedit /etc/sysctl.conf

再最后添加一行如下
fs.inotify.max_user_watches=1048576

reboot
```
