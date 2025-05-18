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

## 磁盘整理
* sudo apt-get install e2fsprogs
* sudo e4defrag /

## 系统日志
* /var/log
* 


