### 安装前要断网
（不然会安装速度特别慢，大概8个小时）
### 更新apt源
见[更新apt源为中国源的方法](https://github.com/meisa233/Working_Notes/blob/main/Latest_apt_sources_in_China.md)
如果出现
```
Could not get lock /var/lib/apt/lists/lock - open (11: Resource temporarily unavailable)
```
这样的bug<br />
解决方法：输入以下命令
```
sudo rm /var/cache/apt/archives/lock
sudo rm /var/lib/dpkg/lock
```
然后查找一下占用apt命令的pid号，并终止
```
ps -e | grep apt
kill -9 pid号
```

参考：https://blog.csdn.net/u010098331/article/details/50782178
