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
#### 2.下载docker的镜像
```
docker pull remie/youtransfer:stable
```
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
···
查看容器ID<br />
得到
```
CONTAINER ID: d7b54f7e235d
```
停止容器，即
```
sudo docker stop CONTAINER ID
```

