# 如何在Ubuntu16.04上安装rsync（本地和远程同步工具）
## 来源：https://blog.csdn.net/apple9005/article/details/82423149
### 1.配置服务器
```
$sudo vi /etc/default/rsync
RSYNC_ENABLE=true   #false改true
```
```
$sudo cp /usr/share/doc/rsync/examples/rsyncd.conf /etc   #已默认安装的软件，默认不启动的似乎都要这么做
```
修改配置文件
```
sudo vi /etc/rsyncd.conf
```
里面的path是同步目录,请自行配置<br />
启动rsync
```
sudo /etc/init.d/rsync start
```
### 2.上传文件到服务器
#### 来源：https://www.liquidweb.com/kb/how-to-securely-transfer-files-via-rsync-and-ssh-on-linux/
```
rsync -avH /home/localuser/testfile1 -e ssh adam@web01.adamsserver.com:/home/adam/testfile1
```
注意，这条命令之后是需要输入密码的
### 3.如何知道命令运行了多久
```
time sh -c '命令内容'
```
