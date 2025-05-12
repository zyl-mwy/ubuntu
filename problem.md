## 进不去桌面，gnome出问题
* sudo apt install --reinstall ubuntu-desktop
* sudo reboot
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



