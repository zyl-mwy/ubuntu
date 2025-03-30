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

* sudo docker pull ubuntu
* 
