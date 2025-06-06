https://www.bilibili.com/video/BV1qNd4YSEMS/?spm_id_from=333.337.search-card.all.click&vd_source=ee200f7e09eb8dbc8631c991d8917853
https://bsdayo.moe/posts/ubuntu-desktop-mac-style/

https://vercel.fallingsakura.top/f24024d4.html#Beautify
* sudo apt install timeshift -y
```
打开软件，设定的用户项选最右边，然后创建一个
```
* sudo apt install gnome-shell-extension-manager gnome-tweaks git curl wget
* sudo apt install flatpak -y
* flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
* sudo reboot now
* https://www.pling.com/p/1102582
```
下载file的第一个，然后解压剪切到home/linxi下的自己建立的.icons(ctrl+H)文件夹
```
* git clone https://github.com/vinceliuice/WhiteSur-wallpapers.git
* cd WhiteSur-wallpapers/
* ls *sh
* sudo ./install-gnome-backgrounds.sh
* ./install-wallpapers.sh
* https://github.com/vinceliuice/WhiteSur-gtk-theme?tab=readme-ov-file#readme
```
复制命令
git clone https://github.com/vinceliuice/WhiteSur-gtk-theme.git --depth=1
```
* cd WhiteSur-gtk-theme/
* ls *sh
* ./install.sh --help
* ./install.sh -a normal -m -N stable -l --round -t all
* sudo ./tweaks.sh -g
* ./tweaks.sh -F -f default
* sudo flatpak override --filesystem=xdg-config/gtk-4.0
```
打开扩展管理器
点击浏览
搜到安装blur my shell
user themes
search light
gnome 4x ui improvements
quick settings tweaker
```
```
打开优化/tweaks
外观中
图标：Cupertino-Sonoma
Shell：WhiteSur-Dark-solid
过时应用程序：WhiteSur-Dark-solid
窗口中
标题栏按钮-放置-左
点击行为-居中显示新窗口-选中
```
```
打开拓展管理器
设置 blur my shell
  面板-管线-default rounded
设置 search light
  general
    search-ctrl+空格
    currency conversion-勾选
    unit conversion-勾选
    icon-勾选
  appearance
    width-0.26
    height-0.40
    border radius-最大
```
```
右击桌面-更改背景
```
* gsettings set org.gnome.shell.extensions.dash-to-dock click-action 'minimize-or-previews'
```
下载拓展
compiz windows effect
compiz alike magic lamp effect
coverflow alt-tab
```
```
设置coverflow alt-tab拓展
  一般
    样式-时间轴
    隐藏面板-取消选中
  图标
    应用图标风格-已吸附
    叠加图标大小-256
```
```
下载拓展
dash to dock
dash2cock animated
network stats
```


## 拓展
* hide top bar
* blur my shell
* forge
* gnome fuzzy app search
* app menu is back
* logo menu
* Quick setting Tweaker
* Compiz alike magic lamp effect
* Compiz windows effect
* Clipboard Indicator
* GSConnect
* Impatience
* Vitals
* Rounded Window Corners
* Burn My Windows
* Desktop Cube

* Space Bar
* dash to panel
* add to desktop
* custom window control

# kubuntu
## 安装
* sudo apt install kubuntu-desktop
## 卸载
* sudo apt remove kubuntu-desktop plasma-desktop
* sudo apt autoremove  # 自动移除不再需要的依赖包
* sudo apt purge plasma* kde* sddm  # 移除 KDE 相关包及其配置文件
* sudo apt autoremove --purge       # 清理残留配置
* sudo apt remove kate konsole dolphin kcalc  # 示例：删除常见 KDE 应用
* ps aux | grep -i plasma
* sudo rm /usr/share/xsessions/plasma*.desktop
* sudo apt --fix-broken install
* sudo apt install ubuntu-desktop  # 确保 GNOME 核心组件完整

* sudo update-alternatives --config default.plymouth
* sudo plymouth-set-default-theme ubuntu-logo
* sudo update-initramfs -u
* sudo apt purge plymouth-theme-kubuntu-logo plymouth-theme-kubuntu-text
* ls /usr/share/plymouth/themes/
* sudo rm -rf /usr/share/plymouth/themes/kubuntu-*
* sudo apt autoremove --purge
* sudo update-initramfs -u

* sudo apt install --reinstall lightdm-gtk-greeter
* sudo apt purge sddm
* sudo apt install gdm3  # 或 lightdm
* sudo dpkg-reconfigure gdm3

## 主题文件夹
* ~/.icons/
* /usr/share/icons/

## 光标主题
* git clone https://github.com/vinceliuice/WhiteSur-cursors.git
* ./install.sh
