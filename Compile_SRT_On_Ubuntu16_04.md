### 安装所需的工具
参考:https://search.gocenter.io/github.com/haivision/srt <br />
https://www.cnblogs.com/djw316/p/10908170.html
#### 1.安装git
```
sudo apt update(请注意如果网速不快需要更改apt源为国内源)
sudo apt upgrade
sudo apt install git
sudo apt-get install tclsh pkg-config cmake libssl-dev build-essential
```
#### 2.克隆SRT库
```
sudo git clone https://github.com/Haivision/srt.git
```
为方便起见，请将srt的权限改为777
#### 3.创建build文件夹
```
cd srt
mkdir build
```
#### 4.配置(在srt文件夹中)
```
./configure --prefix=./build/(build文件夹的路径,注意一下这里最后是有/的) --with-compiler-prefix=/usr/bin/
make
make install
```
