## 进不去桌面，gnome出问题
* sudo apt install --reinstall ubuntu-desktop
* sudo reboot
## ubuntu磁盘修复
1. ubuntu
* sudo apt update
* sudo apt install ntfs-3g
* sudo ntfsfix -d /dev/nvme0n1p3
2. windows
* chkdsk /f X:


## ubuntu硬盘挂载不上
* lsblk
* sudo blkid /dev/nvme0n1p3
* sudo mount -t ntfs(ext4) /dev/nvme0n1p3 /media/linxi
## ubuntu硬盘不能自动挂载--开机自启动
* sudo nano /etc/systemd/system/mount-ntfs.service
```
[Unit]
Description=Mount NTFS Partition
After=network.target

[Service]
Type=oneshot
ExecStart=/bin/mount -t ntfs /dev/nvme0n1p3 /media/linxi
TimeoutSec=0
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```
* sudo systemctl daemon-reload
* sudo systemctl enable mount-ntfs.service
## desktop error
* dconf reset -f /org/gnome/
* sudo apt install --reinstall ubuntu-desktop gnome-shell
## 中英文用户文件夹混乱
* LC_ALL=C xdg-user-dirs-update --force
* LANG=zh_CN.UTF-8 xdg-user-dirs-update --force

## 磁盘整理
* sudo apt-get install e2fsprogs
* sudo e4defrag /
## 开机引导项问题
* sudo update-grub

## 多屏幕无法镜像
* sudo apt install --reinstall libgl1-mesa-dri mesa-vulkan-drivers xserver-xorg-video-intel
* rm ~/.config/monitors.xml
* sudo rm /var/lib/gdm3/.config/monitors.xml

## ibus-libpinyin出问题
* ibus restart
* sudo apt update
* sudo apt upgrade
* sudo apt install --reinstall ibus-libpinyin
* sudo apt install -f
* rm -rf ~/.cache/ibus ~/.config/ibus
* ibus-daemon -drx

## 双系统时间不同步
* sudo timedatectl set-local-rtc 1

## 更新错误
```
W: 校验数字签名时出错。此仓库未被更新，所以仍然使用此前的索引文件。GPG 错误：https://apt.v2raya.org v2raya InRelease: GPG: add_keyblock_resource 33587281  GPG: keydb_search 33554445  GPG: keydb_search 33554445
W: 无法下载 https://apt.v2raya.org/dists/v2raya/InRelease  GPG: add_keyblock_resource 33587281  GPG: keydb_search 33554445  GPG: keydb_search 33554445
W: 部分索引文件下载失败。如果忽略它们，那将转而使用旧的索引文件
```
* sudo rm /etc/apt/sources.list.d/v2raya.list
* sudo rm /etc/apt/sources.list.d/v2raya.list.save

## 系统日志
### 日志保存位置
* /var/log
### 日志系统
* 软件包: rsyslog
* 主要程序: /sbin/rsyslogd
* 配置文件: /etc/rsyslog.conf
### 日志级别
* 0 EMERG (紧急) : 会导致主机系统不可用的情况
* 1 ALERT (警告) : 必须马上采取措施解决问题
* 2 CRIT (严重) : 比较严重的情况
* 3 ERR (错误) : 运行出现错误
* 4 WARNING (提醒) : 可能会影响系统功能的事件
* 5 NOTICE (注意) : 不会影响系统但值得注意
* 6 INFO (信息) : 一般信息
* 7 DEBUG (调试) : 程序或系统调试信息等
### 查看日志
* more /xxx
* gnome-logs

### 关机很慢
* 查看关机内容
```bash
sudo vim /etc/default/grub
```
将
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
```
改为
```
GRUB_CMDLINE_LINUX_DEFAULT=""
```
然后更新grub
```
sudo update-grub
```

* 修改关机文件
```bash
sudo vim /etc/systemd/system.conf 
```
修改一下内容
```
#DefaultTimeoutStartSec=90s
#DefaultTimeoutStopSec=90s
```
为
```
DefaultTimeoutStartSec=3s   #这个最好不要启用，启用后可能出现fstab中的硬盘不能自动挂载，grub菜单不能隐藏的问题
DefaultTimeoutStopSec=1s  # 将#去掉，90改为1
```
最后加载修改的配置
```bash
systemctl daemon-reload
```
