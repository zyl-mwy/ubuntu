* 切换国内源
* 启用ubuntu pro
* 更新包
```
sudo apt update && sudo apt upgrade
```
* 调整隐私设置 
```
sudo ubuntu-report -f send no
```
* 配置 TLP
```
sudo apt install tlp
```
* 第三方软件包管理器 
```
sudo apt install gdebi
sudo apt install synaptic
```
* 安装 Flatpak 并启用 Flathub
```
# 安装 Flatpak
sudo apt install flatpak
# 添加上海交大软件源
sudo flatpak remote-add --if-not-exists flathub https://mirror.sjtu.edu.cn/flathub
# 重启系统
reboot
```
* 移除 Snap 版 Firefox 和 Thunderbird，换回 deb 版
```
sudo snap remove --purge firefox thunderbird
sudo apt remove --purge firefox thunderbird
sudo add-apt-repository ppa:mozillateam/ppa


echo '
Package: *
Pin: release o=LP-PPA-mozillateam
Pin-Priority: 1001
' | sudo tee /etc/apt/preferences.d/mozillateamppa

sudo apt update
sudo apt install firefox thunderbird
```
* 安装额外软件和字体
```
sudo apt install ubuntu-restricted-extras
sudo apt install gimp vlc synaptic
sudo apt install fonts-noto-cjk-extra fonts-roboto fonts-cascadia-code fonts-firacode
```
* 安装备份工具
```
sudo apt install timeshift
```



