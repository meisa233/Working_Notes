### 1.下载msys2

msys2的官网
```
https://www.msys2.org/
```
msys2为在Ubuntu下编写的工具提供了环境<br />

#### msys2的安装
##### 安装包列表
```
http://repo.msys2.org/distrib/x86_64/
```
这里选择的**msys2-x86_64-20200903.exe**<br />
直接进行安装，注意安装路径不要有任何中文，最好就是纯英文。<br />
### 2.安装srt-file-transmit
包的地址
```
https://packages.msys2.org/package/mingw-w64-x86_64-srt?repo=mingw64
```
以管理员权限打开msys2(C:\msys64\msys2.exe)<br />
安装srt-file-transmit所在的工具包
```
pacman -S mingw-w64-x86_64-srt
```
### 3.运行srt-file-transmit

在cmd（管理员运行）窗口中，找到srt-file-transmit.exe，直接运行
```
C:\msys64\mingw64\bin\srt-file-transmit.exe
```
transmit-file-srt命令行基本用法，windows上（发送端）
```
srt-file-transmit.exe "file://文件地址（注意分隔符是/） srt://目标ip:目标ip的端口号
```
注意，在windows上，cmd中当前的目录应当是要传送的文件所在的目录，比如你要传送c盘下的某个文件，就需要切换到c盘，然后再执行上面的命令，例子
```
srt-file-transmit.exe "file://C:/srt_transmit_test.png" srt://192.168.32.131:5002
```
接收端（Ubuntu为例）
```
./srt-file-transmit（srt-file-transmit的地址） srt://5002（端口号）/?mode=listener file:///tmp/（接收地址）
```
ps:加上在运行srt-file-transmit时加上选项-v可以得到更详细的输出。
