## 进不去桌面，gnome出问题
* sudo apt install --reinstall ubuntu-desktop
* sudo reboot
## ubuntu硬盘挂载不上
* lsblk
* sudo blkid /dev/nvme0n1p3
* sudo mount -t ntfs(ext4) /dev/nvme0n1p3 /media/linxi
