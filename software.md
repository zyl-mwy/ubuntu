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
* sudo apt clearn
* dpkg -l|grep ^rc|awk '{print $2}' |sudo xargs dpkg -P
​* rm -rfv ~/.wine
* ls .local/share/applications/
* ls .config/menus/applications-merged/
* ls .local/share/icons/
* sudo find / -name *wine*

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

## common
* wps
* bandizip
* stacer
* 星火应用商店
* 应用管理器
* 百度网盘
* 嘉立创
* 微信
* edge
* todesk
* v2ray
* vscode
* vim
* zotero
* 7zip
* virtualbox

## fast access
* 全局菜单项：/usr/share/applications/
* 个人菜单项：~/.local/share/applications/

## windows
* win32diskmanager
* rufus
* office+visio
* adobe
* mathtype
* 
