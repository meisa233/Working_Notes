# 请不要尝试升级Ubuntu系统本身自带的Python3
## 请选择在Ubuntu系统中多版本共存
由于Ubuntu的很多包依赖于系统预安装好的python3.5，升级之后，系统本身的/usr/bin/python3所指向的python版本改变，很多包会安装不上的！！！
<br />
### 1.python多版本管理：
https://www.cnblogs.com/jasonboboblog/p/12375370.html
### 2.安装新python
来源:[cnblogs的一篇博文](https://www.cnblogs.com/jsdy/p/12694908.html)
#### (1)更新apt
[建议换成国内源](https://github.com/meisa233/Working_Notes/blob/main/Latest_apt_sources_in_China.md)
```
sudo apt update
sudo apt upgrade
```
如果有询问是否要升级当前包的选项，请选择保持（Keep）当前版本的选项。
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
make -j8 # -j8会加速
sudo make install
```
#### (5)新建软连接
##### 注意最后一个参数不要与系统本身存在的软连接名字相同!
```
#添加python3的软链接
sudo ln -s /usr/local/python3/bin/python3.8 /usr/bin/python3.8
#添加 pip3 的软链接
sudo ln -s /usr/local/python3/bin/pip3.8 /usr/bin/pip3.8
```
#### (6)检测版本
```
python3.8 -V
pip3.8 -V
```

### 3.bug:apt安装失败，Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend)
https://blog.csdn.net/shimadear/article/details/90598646
