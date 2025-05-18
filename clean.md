* sudo apt autoclean    # 清理旧版本的软件包缓存
* sudo apt autoremove  # 删除不再需要的依赖包
* sudo apt clean       # 彻底清理所有软件包缓存
* sudo journalctl --vacuum-size=100M  # 限制日志大小为100MB
* rm -rf ~/.cache/*    # 用户缓存
* sudo rm -rf /var/cache/*  # 系统缓存（谨慎操作）
* sudo apt purge $(dpkg -l | grep 'linux-image.*unsigned' | awk '{print $2}')  # 删除旧内核
* sudo apt install stacer
* sudo apt install bleachbit
* sudo apt install fslint
* sudo snap refresh --list   # 查看可更新的 Snap
* sudo snap remove --purge <包名>  # 彻底删除 Snap 包
* flatpak uninstall --unused  # 删除未使用的运行时
