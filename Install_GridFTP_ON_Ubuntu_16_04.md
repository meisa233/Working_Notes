## 官方主页：https://gridcf.org/gct-docs/6.2/gridftp/index.html
## gridftp-admin主页：https://gridcf.org/gct-docs/6.2/gridftp/admin/index.html
## 安装介绍：https://gridcf.org/gct-docs/6.2/admin/install/index.html
## deb文件列表：https://downloads.globus.org/toolkit/gt6/stable/installers/repo/deb/index.html
## 安装步骤
### 1.下载安装包并安装
```
wget https://downloads.globus.org/toolkit/gt6/stable/installers/repo/deb/globus-toolkit-repo_latest_all.deb
sudo dpkg -i globus-toolkit-repo_latest_all.deb
sudo apt update
sudo apt install globus-gridftp
```
### 2.配置gridftp的ssh
官方有关gridftp的介绍
```
Configure Server for SSH GridFTP Support
Every host that wishes to run a globus-gridftp-server which can accept sshftp:// connections must run the following command as root: connections must run the following command as root:

globus% globus-gridftp-server-enable-sshftp
In the absence of root access, a user can configure the server to allow sshftp:// connections for that user only with the following command: connections for that user only with the following command:

globus% globus-gridftp-server-enable-sshftp -nonroot
The above command creates a file named sshftp in /etc/grid-security (if run as root) or in $HOME/.globus (if run as nonroot). You may edit this file to set gridftp commandline options or environment variables such as GLOBUS_TCP_PORT_RANGE, but you can also set those options in the config file.

Performing sshftp:// Transfers Transfers
In this case, a globus-gridftp-server does not need to be running. The server will be started via the sshd program. Therefore, the hostname and port should be that of the sshd server. Run globus-url-copy just as you have before; simply change ftp:// to to sshftp://..

globus% globus-url-copy -v file:/etc/group sshftp://127.0.0.1/tmp/group
globus% globus-url-copy -list sshftp://127.0.0.1/tmp/
```
进入root用户，输入以下命令
```
 globus-gridftp-server-enable-sshftp
```
可修改配置文件/etc/grid-security/sshftp
### 3.使用说明
官方的用户文档
https://gridcf.org/gct-docs/6.2/gridftp/user/index.html
简单的example:
```
globus-url-copy -vb -p 8 file:/path/to/local/file sshftp://username@remoteurl/path/to/remote/folder
```
```
-vb
specifies verbose mode and displays:

number of bytes transferred,

performance since the last update (currently every 5 seconds), and

average performance for the whole transfer.

-p
Specifies the number of parallel data connections that should be used. This is one of the most commonly used options.
```
