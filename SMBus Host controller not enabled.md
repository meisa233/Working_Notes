# Linux中开机出现“piix4_smbus 0000:00:07.3: SMBus Host controller not enabled”问题解决方式
## 问题及解决来源：https://blog.csdn.net/qq_41128018/article/details/88175065
### 解决方案
```
1.查明装入模块的名字：lsmod | grep i2c

2.将该模块列入不装入名单：gedit /etc/modprobe.d/blacklist.conf

在文件最后一行加：blacklist i2c_piix4

3.重新生成引导文件：sudo update-initramfs -u -k all

4.重启：reboot
```
