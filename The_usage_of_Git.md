# 如何使用Git（命令行）
## 教程来源：https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/585490/
### 1.创建ssh-key
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
# Creates a new ssh key, using the provided email as a label
```
其中your_email@example.com是用于登陆github的邮箱<br />
之后一路回车就可以了
### 2.将ssh-key添加至ssh代理中
#### a.确保ssh代理正在运行
```
eval "$(ssh-agent -s)"
Agent pid 59566
```
#### b.将ssh-key（私钥）加入到ssh代理中
```
ssh-add ~/.ssh/id_rsa
```
### 3.将公钥添加至github账户中
右上角个人账号-->【settings】-->【SSH and GPG Keys】-->【new SSH keys】-->复制~/.ssh/id_rsa.pub中的【全部内容】至KEY域中-->Title随便写
### 4.设定全局账号信息
```
git config --global user.name “lukeyan”
git config --global user.email xxx@gmail.com
```
### 5.测试登陆是否成功
```
ssh -T git@github.com
```
### 6.push代码
切换到代码的主目录下
```
git init（如果代码目录下没有.git文件夹请输入此命令）
git pull #獲取新版本
git status #獲取需要上傳的檔案 
git add . # .表示全新增， git add README.md 表示只新增說明檔案
git commit -m "add new files" # a commit
git remote add origin git@github.com:yourgithubname/yourrepositoryname
git remote remove(如果输入remote地址错误 或 需更改remote地址，请输入这个命令）
git push -u origin master
```
## 更新git版本
```
sudo add-apt-repository ppa:git-core/ppa
中间暂停时，按回车键Enter继续安装…
sudo apt-get update
sudo apt-get install git
```
