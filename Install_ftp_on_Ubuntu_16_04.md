# 如何配置ftp服务
## 教程来源：https://www.cnblogs.com/gtx159/p/11243122.html
### 1.安装vsftpd
```
sudo apt update
sudo apt install vsftpd
```
### 2.重启
```
sudo shutdown -r now
```
### 3.创建ftp用户
```
sudo passwd ftp
```
### 4.创建ftp用户的家目录
```
sudo mkdir /home/ftp
sudo chmod 777 /home/ftp
```
### 5.修改配置文件
```
sudo gedit /etc/vsftpd.conf
```
```
将配置文件中”anonymous_enable=YES “改为 “anonymous_enable=NO”（是否允许匿名ftp，若不允许选NO）
取消如下配置前的注释符号：
local_enable=YES（是否允许本地用户登录）
write_enable=YES（是否允许本地用户写的权限）
chroot_local_user=YES（是否将所有用户限制在主目录）
chroot_list_enable=YES（是否启动限制用户的名单）
chroot_list_file=/etc/vsftpd.chroot_list（可在文件中设置多个账号）
```
### 6.添加可登陆用户
新建chroot_list_file=后面跟的那个文件，在里面添加可登录用户的用户名
### 7.重启ftp服务
```
sudo service vsftpd restart
```
### 8.服务器登录
```
命令行中输入ftp localhost
然后输入步骤6中的用户名和密码
```
### 9.客户端
```
ftp
>open 服务器的ip地址
```
### 10.Windows上的使用
```
ftp
open <ip_addr>
put <source file> [target file (name)]
bye
```
