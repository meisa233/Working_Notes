### 1.安装新python
来源:[cnblogs的一篇博文](https://www.cnblogs.com/jsdy/p/12694908.html)
#### (1)更新apt
[建议换成国内源](https://github.com/meisa233/Working_Notes/blob/main/Latest_apt_sources_in_China.md)
```
sudo apt update
```
#### (2)安装依赖库
```
sudo apt-get install zlib1g-dev libbz2-dev libssl-dev libncurses5-dev libsqlite3-dev libreadline-dev tk-dev libgdbm-dev libdb-dev libpcap-dev xz-utils libexpat1-dev liblzma-dev libffi-dev libc6-dev
```
↑这一步出问题，提示无法安装各种依赖需要手动安装的情况的话，建议重装系统。
#### (3)下载python安装包
在[python官网](https://www.python.org/downloads/)下载需要安装的版本(源码），一般是后缀为.tgz的文件
#### (4)解压与安装
```
tar zxvf Python-3.8.2.tgz #解压
```
```
cd Python-3.8.2
sudo mkdir -p /usr/local/python3 #建立安装目录

#后面加上 --enable-optimizations 会自动安装pip3及优化配置
./configure --prefix=/usr/local/python3  --enable-optimizations
make
sudo make install
```
#### (5)删除软连接
```
sudo rm -rf /usr/bin/python3
sudo rm -rf /usr/bin/pip3
```
#### (6)新建软连接
```
#添加python3的软链接
sudo ln -s /usr/local/python3/bin/python3.8 /usr/bin/python3
#添加 pip3 的软链接
sudo ln -s /usr/local/python3/bin/pip3.8 /usr/bin/pip3
```
#### (7)检测版本
```
python3 -V
pip3-V
```
### 2.删除lsb_release
来源:https://github.com/pypa/pip/issues/4924<br />
不完成这步的话，在使用```pip3 install xxx(库名称)```时会出现
```
return Command 'lsb_release -a' returned non-zero exit status 1.
```
这样的问题，PyCharm是无法创建虚拟环境的。
命令如下：
```
sudo rm /usr/bin/lsb_release
```
### 3.修复Ctrl + Alt + T快捷键
由于终端依赖于python3.5，因此在修改python3的版本之后，该快捷键失效，所以现在需要将python3的挂载点修改为python3.5<br />
修改方法：
```
cd /usr/bin
sudo gedit gnome-terminal
```
将开头的第一行中的```#!/usr/bin/python3```修改为```#!/usr/bin/python3.5```
