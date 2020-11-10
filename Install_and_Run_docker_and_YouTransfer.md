### YouTransfer官网
```
https://github.com/YouTransfer/YouTransfer
```
### 安装方式
#### 1.安装docker(在Ubuntu 16.04上)
##### (1) docker官网
```
https://docs.docker.com/get-docker/
```
##### (2) 通过apt安装docker
```
$ sudo apt-get update

$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```

```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
通过搜索指纹（9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88）的后8个字符，验证您现在是否拥有带有指纹的密钥 
```
$ sudo apt-key fingerprint 0EBFCD88

pub   rsa4096 2017-02-22 [SCEA]
      9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
sub   rsa4096 2017-02-22 [S]
```
```
 $ sudo apt-get update
 $ sudo apt-get install docker-ce docker-ce-cli containerd.io
```
测试docker是否能正常运行
```
sudo docker run hello-world
```
##### 容易出现的bug
###### 1.无法找到相应的包
以下bug在输入
```
 $ sudo apt-get install docker-ce docker-ce-cli containerd.io
```
出现
```
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Package docker-ce is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source

E: Package 'docker-ce' has no installation candidate
E: Unable to locate package docker-ce-cli
E: Unable to locate package containerd.io
E: Couldn't find any package by glob 'containerd.io'
E: Couldn't find any package by regex 'containerd.io'
```
解决方法（来源：https://elementaryos.stackexchange.com/questions/22040/installing-docker-community-edition-fails-with-missing-docker-ce-package）
```
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```
#### 2.下载docker的镜像
```
docker pull remie/youtransfer:stable
```
在国内的话，pull会比较慢，所以我们修改一下pull的源
```
[root@localhost ~]# /etc/docker
[root@localhost ~]# vi /etc/docker/daemon.json
{
"registry-mirrors": ["https://9cpn8tt6.mirror.aliyuncs.com"]
}

[root@localhost ~]# systemctl daemon-reload
[root@localhost ~]# systemctl restart docker
```
↑该命令需要以root身份运行
#### 3.运行docker
```
docker run -d \
-v [path_to_upload_folder]:/opt/youtransfer/uploads \
-v [path_to_config_folder]:/opt/youtransfer/config \
-p 80:5000 \
remie/youtransfer:stable
```
#### 4.停止docker
```
sudo docker ps
```
查看容器ID<br />
得到
```
CONTAINER ID: d7b54f7e235d
```
停止容器，即
```
sudo docker stop CONTAINER ID
```

