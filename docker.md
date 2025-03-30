from https://blog.csdn.net/u011278722/article/details/137673353

## 卸载默认
* sudo apt-get remove docker docker-engine docker.io containerd runc

## 安装必要支持
* sudo apt install apt-transport-https ca-certificates curl software-properties-common gnupg lsb-release

## GPG key
* curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
* curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

## apt 源
* echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
* echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

## 更新源
* sudo apt update
  
* sudo apt-get update

## 安装docker
* sudo apt install docker-ce docker-ce-cli containerd.io

* sudo docker version

* sudo systemctl status docker

## 安装Docker 命令补全工具
* sudo apt-get install bash-completion

* sudo curl -L https://raw.githubusercontent.com/docker/docker-ce/master/components/cli/contrib/completion/bash/docker -o /etc/bash_completion.d/docker.sh
* wget https://raw.githubusercontent.com/docker/docker-ce/master/components/cli/contrib/completion/bash/docker -o docker.sh
* 挂梯子下载好放在这

* source docker.sh

## 添加docker用户组
* sudo groupadd docker

## 将当前用户添加到用户组
* sudo usermod -aG docker $USER

## 使得权限生效
* newgrp docker

## .bashrc 添加内容
```
groupadd -f docker
```
* source .bashrc

## 查看所有容器
* docker ps -a





* sudo docker pull ubuntu
* 
