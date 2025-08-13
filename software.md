## apt/apt-get update
* sudo apt update
* sudo apt upgrade
* sudo apt dist-upgrade
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
```
sudo apt/snap remove firefox
cd ~/Downloads
tar -jxvf Firefox-latest-x86_64.tar.bz2
sudo mv firefox /opt
/opt/firefox/firefox
cd /usr/share/applications
sudo vi firefox.desktop

[Desktop Entry]
Name=firefox
Name[zh_CN]=火狐浏览器
Comment=火狐浏览器
Exec=/opt/firefox/firefox
Icon=/opt/firefox/browser/chrome/icons/default/default128.png
Terminal=false
Type=Application
Categories=Application;
Encoding=UTF-8
StartupNotify=true

ls /usr/share/applications/ | grep firefox
sudo update-desktop-database
gnome-shell --replace &
```
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
* synaptic 商店
* discover 商店
* flatpak 商店
```
sudo apt install flatpak
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
https://flathub.org/

sudo apt install flatpak
sudo apt install gnome-software-plugin-flatpak
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```
* snap-store
* appimagelauncher
* software-properties-gtk
* gxde-app-upgrader

* deborphan
* GtkOrphan

## bigger disk
* EaseUS Partition Master
* gparted

## chinse
* sudo apt update
* sudo apt install ibus ibus-pinyin
* im-config
* 注销
* 键盘布局

/usr/share/applications
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
* dpkg --list | grep yed

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

## uninstall steam
* sudo apt remove --purge steam steam-launcher
* sudo dpkg -r steam
* rm -rf ~/.steam
* rm -rf ~/.local/share/Steam
* sudo rm -rf /usr/share/steam
* sudo rm /etc/apt/sources.list.d/steam.list
* sudo rm /etc/apt/trusted.gpg.d/steam.gpg  # 如果存在

## uninstall wine
* apt list --installed | sed -E 's|(.*)/.*|\1|' | grep -i wine
* sudo apt purge
* apt list --installed | sed -E 's|(.*)/.*|\1|' | grep -i wine
* sudo -l | grep ^rc |awk '{print $2}' | sudo xargs dpkg -P
* sudo apt autoremove 
* sudo apt autoclean 
* sudo apt clean
* dpkg -l|grep ^rc|awk '{print $2}' |sudo xargs dpkg -P
​* rm -rfv ~/.wine
* ls .local/share/applications/
* ls .config/menus/applications-merged/
* ls .local/share/icons/
* sudo find / -name *wine*

* sudo rm -rf opt/deepinwine

* sudo rm /etc/apt/sources.list.d/winehq-*.list
* sudo apt update
* sudo snap remove wine-platform-runtime

## uninstall snap-store
https://zhuanlan.zhihu.com/p/511438456
* sudo snap remove snap-store
* snap list
* sudo snap remove <package-name>
* sudo apt purge snapd
* sudo rm -rf /var/snap /var/lib/snapd /var/cache/snapd /usr/lib/snapd ~/snap
* sudo apt-mark hold snapd

* sudo systemctl disable --now snapd.service snapd.socket snapd.seeded.service
* sudo apt install --reinstall gnome-software

## uninstall snap
* snap list

* sudo snap remove --purge firefox
* sudo snap remove --purge snap-store
* sudo snap remove --purge gnome-3-38-2004
* sudo snap remove --purge gtk-common-themes
* sudo snap remove --purge snapd-desktop-integration
* sudo snap remove --purge bare
* sudo snap remove --purge core20
* sudo snap remove --purge snapd

* sudo apt remove --autoremove snapd

* sudo gedit /etc/apt/preferences.d/nosnap.pref
```
Package: snapd
Pin: release a=*
Pin-Priority: -10
```

* sudo apt update

* sudo apt install --install-suggests gnome-software

* sudo add-apt-repository ppa:mozillateam/ppa
* sudo apt update
* sudo apt install -t 'o=LP-PPA-mozillateam' firefox

* echo 'Unattended-Upgrade::Allowed-Origins:: "LP-PPA-mozillateam:${distro_codename}";' | sudo tee /etc/apt/apt.conf.d/51unattended-upgrades-firefox

* sudo gedit /etc/apt/preferences.d/mozillateamppa
```
Package: firefox*
Pin: release o=LP-PPA-mozillateam
Pin-Priority: 501
```

## 卸载edge
* sudo apt remove --purge microsoft-edge-stable
* rm -rf ~/.config/microsoft-edge
* rm -rf ~/.cache/microsoft-edge
* sudo rm -f /etc/apt/sources.list.d/microsoft-edge.list
* sudo rm -f /usr/share/keyrings/microsoft-edge.gpg
* sudo apt autoremove

## 卸载virtualbox
* sudo apt-get remove --purge virtualbox-\*
* sudo apt-get autoremove
* sudo rm -rf ~/.config/VirtualBox/
* sudo rm -rf ~/.VirtualBox/
* sudo rm -rf /etc/vbox/
* sudo rm -rf ~/VirtualBox VMs/
* sudo dpkg -r virtualbox-<version>
* virtualbox --version

## 卸载python2.7
* which python2.7
* sudo find /usr/local -name "*python2.7*"
* sudo rm -rf /usr/local/lib/python2.7/
* sudo rm -f /usr/local/bin/python2.7*
* sudo rm -f /usr/local/bin/python2*  # 如果存在
* sudo rm -rf /usr/local/share/doc/python2.7/
* sudo rm -rf /usr/local/share/examples/python2.7/
* which python2.7

## 卸载flatpak
* flatpak uninstall --all
* sudo apt remove flatpak
* sudo flatpak remote-delete flathub
* rm -rf ~/.local/share/flatpak
* sudo rm -rf /var/lib/flatpak
* sudo apt autoremove
* flatpak --version

## 卸载xdroid
* sudo rm -rf /opt/xdroid
* rm -rf ~/xdroid
* rm -rf ~/.xdroid
* rm -rf ~/.zhuoyi
* rm -rf /usr/share/applications/xDroid.desktop
* cd /usr/src
* sudo rm -rf \*xdroid\*
* cd /lib/systemd/system/
* sudo rm -rf xdroid*
* sudo systemctl daemon-reload
* cd /etc/udev/rules.d
* sudo rm -rf \*xdroid\*

## 卸载tlp
* sudo apt remove --purge tlp tlp-rdw
* sudo apt install power-profiles-daemon  # 确保默认电源管理服务已安装
* sudo systemctl restart power-profiles-daemon

## common
* latex
* wps
* bandizip
* stacer
* gparted
* 星火应用商店/Synaptic Package Manager/discover/自带
* 应用管理器
* 拓展管理器
* 百度网盘
* 嘉立创
* 微信
* edge/火狐
* todesk
* v2raya
* vscode
* vim
* zotero
* 7zip
* virtualbox
* telegram
* 视频
* anaconda
* timeshift
* yEd Graph Editor
* qq
* 安卓模拟器 https://www.linzhuotech.com/Product/download
* 录屏
```
sudo add-apt-repository ppa:obsproject/obs-studio
sudo apt install obs-studio
```
* 任务中心/系统监视中心
* flix
* AI工具
* vlc
* 玲珑应用商店
* clash-verge
```
https://github.com/zzzgydi/clash-verge/releases/
```
* bleachbit
* steam++
```
curl -sSL https://steampp.net/Install/Linux.sh | bash
```
* kdeconnect
* fslint
*  QEMU + KVM 虚拟机
```
LC_ALL=C lscpu | grep Virtualization
egrep -c '(vmx|svm)' /proc/cpuinfo

sudo apt install qemu qemu-kvm virt-manager bridge-utils

sudo useradd -g $USER libvirt
sudo useradd -g $USER libvirt-kvm

sudo systemctl enable libvirtd.service && sudo systemctl start libvirtd.service
```
* psensor
```
sudo apt install -y psensor
```

## 系统安装
* efi系统分区 500MB
* swap 20GB/大于内存
* /root/home
* /

## fast access
* 全局菜单项：/usr/share/applications/
* 个人菜单项：~/.local/share/applications/

## 软件安装位置
* /opt
* /usr/local

## 查找安装包
* dpkg -l | grep python2.7
* dpkg -L python2.7
* whereis python2.7
* where python2.7
* sudo find / -type f -name "\*python2.7\*" 2>/dev/null
* sudo find /usr/local -type f -name "*python2.7*" 2>/dev/null

## windows
* win32diskmanager
* rufus
* office+visio
* adobe
* mathtype

## 常用软件打开命令
* nautilus 文件管理器
```
nautilus admin:/
```
* gnome-control-center 设置
* gnome-system-monitor 任务中心

## reset apt
* sudo apt purge gnome-terminal -y  # 彻底删除配置和软件包
* sudo apt autoremove -y  # 删除不再需要的依赖项
* rm -rf ~/.config/dconf/user  # 重置 GNOME Terminal 配置（谨慎操作！）
* sudo apt update && sudo apt install gnome-terminal -y

## 添加或卸载软件源头
### 添加
* sudo add-apt-repository ppa:wireshark-dev/stable
### 删除
* sudo add-apt-repository --remove ppa:wireshark-dev/stable
或者
* cd /etc/apt/sources.list.d
* sudo rm wireshark-dev-ubuntu-stable-*.list
