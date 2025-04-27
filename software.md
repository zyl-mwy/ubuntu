## apt/apt-get update
* sudo apt update
* sudo apt upgrade
* sudo apt-get update
* sudo apt-get ungrade

## fix
* sudo apt --fix-broken install
* sudo dpkg --configure -a
* sudo apt clean
* sudo apt autoclean

## from apt-get
* htop
* net-tools
* sudo apt install curl software-properties-common apt-transport-https ca-certificates
* wget
* tree
* tmux 终端复用
* screen 终端会话管理
* chromium-browser
  
* git
* build-essential
* cmake
* python3-pip
* g++
* openjdk-11-jdk
* openjdk-17-jdk
* nodejs npm

* openssh-server
* nmap 网络扫描工具
* traceroute
* telnet
* dnsutils DNS工具

* vim
* nano
* emacs

* zip unzip
* tar
* rar unrar
* p7zip-full

* ffmpeg
* vlc
* imagemagick

* docker.io
* virtualbox

* firefox
* chromium-browser

* gparted 磁盘分区
* neofetch 系统信息展示工具
* rsync 文件同步工具
* jq 格式化工具

* octave 开源的 MATLAB 替代工具
* r-base

* stacer https://github.com/oguzhaninan/Stacer/releases 清理
* synaptic sudo apt install -y synaptic 软件管理
* 星火应用商店
* plasma-discover 商店

* deborphan
* GtkOrphan
* gparted


## apt/apt-get install/uninstall 
* sudo apt search xxx
* sudo apt-get install xxx
* sudo apt install xxx
* sudo apt remove xxx
* sudo apt autoremove
* sudo apt purge xxx
* sudo apt autopurge

## dpkg
* sudo dpkg -i xxx*.deb
* sudo dpkg -r xxx
* sudo dpkt -P xxx

## fix2

* sudo rm /var/lib/apt/lists/lock
* sudo rm /var/lib/dpkg/lock
* sudo rm /var/lib/dpkg/lock-frontend
* sudo dpkg --configure -a
* sudo apt clean
* sudo apt update --fix-missing
* sudo apt install -f
* sudo dpkg --configure -a
* sudo apt upgrade
* sudo apt dist-upgrade
