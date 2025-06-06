# Ubuntu 系统故障排查指南
当 Ubuntu 系统出现问题时，系统化的排查方法能帮助你快速定位和解决问题。以下是详细的故障排查流程：
## 一、基础系统状态检查
### 1. 系统资源检查
```bash
# 查看系统负载
uptime

# 查看CPU使用情况
mpstat -P ALL 1  # 需安装 sysstat
top

# 查看内存使用
free -h
vmstat 1

# 查看磁盘I/O
iostat -xz 1
iotop  # 需安装 iotop
```
### 2. 存储空间检查
```
# 检查磁盘空间
df -hT

# 检查inode使用
df -i

# 查找大文件
sudo du -sh /* | sort -rh
sudo du -sh /var/* | sort -rh
```
## 二、日志分析
### 1. 系统日志
```
# 查看系统日志
sudo journalctl -xe
sudo journalctl -p err -b  # 本次启动的错误

# 查看特定服务的日志
sudo journalctl -u nginx --since "1 hour ago"
```
2. 关键日志文件
```
# 系统主日志
tail -f /var/log/syslog

# 认证日志
tail -f /var/log/auth.log

# 内核日志
dmesg | less
cat /var/log/kern.log

# 启动日志
cat /var/log/boot.log
```
## 三、服务管理
### 1. 服务状态检查
```
# 列出所有服务状态
systemctl list-units --type=service --all

# 查看失败的服务
systemctl --failed

# 检查服务依赖关系
systemctl list-dependencies nginx
```
### 2. 服务调试
```
# 查看服务状态详情
systemctl status nginx -l

# 重新加载服务配置
systemctl daemon-reload

# 重置失败的服务状态
systemctl reset-failed
```
## 四、网络问题排查
### 1. 基础网络检查
```
# 网络接口状态
ip addr show
ip link show

# 路由表
ip route show

# DNS解析
dig example.com
nslookup example.com
```
### 2. 连接测试
```
# 测试网络连通性
ping -c 4 8.8.8.8
traceroute 8.8.8.8

# 测试端口连通性
telnet example.com 80
nc -zv example.com 80
```
### 3. 防火墙检查
```
# UFW防火墙状态
sudo ufw status verbose

# iptables规则
sudo iptables -L -n -v
```
## 五、硬件相关问题
### 1. 硬件信息
# CPU信息
```
lscpu
cat /proc/cpuinfo

# 内存信息
sudo dmidecode --type memory

# 磁盘信息
lsblk -o NAME,FSTYPE,SIZE,MOUNTPOINT
sudo hdparm -I /dev/sda
```
### 2. 硬件错误检查
```
# 检查内核硬件错误
dmesg | grep -i error

# 检查磁盘SMART状态
sudo smartctl -a /dev/sda
```
## 六、常见问题解决方案
### 1. 系统无法启动
```
# 进入恢复模式后：
fsck -y /dev/sda1  # 修复文件系统
mount -o remount,rw /  # 重新挂载为可写
dpkg --configure -a  # 修复未完成的包安装
```
### 2. 软件包问题
# 修复损坏的包
```
sudo apt --fix-broken install
sudo dpkg --configure -a

# 清理包缓存
sudo apt clean
sudo apt autoclean
```
### 3. 性能问题
```
# 检查系统限制
ulimit -a

# 查看高资源占用进程
ps aux --sort=-%cpu | head
ps aux --sort=-%mem | head
```
## 七、高级调试工具
### 1. 进程调试
```
# 跟踪系统调用
strace -p <PID>

# 跟踪库调用
ltrace -p <PID>
```
### 2. 性能分析
```
# 系统性能快照
sudo perf stat -a sleep 10

# CPU火焰图
git clone https://github.com/brendangregg/FlameGraph
perf record -F 99 -a -g -- sleep 60
perf script | ./FlameGraph/stackcollapse-perf.pl | ./FlameGraph/flamegraph.pl > perf.svg
```
## 八、系统恢复技巧
### 1. 从Live CD恢复
```
# 挂载原系统分区
sudo mount /dev/sda1 /mnt
sudo mount --bind /dev /mnt/dev
sudo mount --bind /proc /mnt/proc
sudo mount --bind /sys /mnt/sys
sudo chroot /mnt
```
### 2. 重要文件备份
```
# 备份关键配置文件
sudo tar czvf config_backup.tar.gz /etc /var/lib/dpkg /var/lib/apt/extended_states
```
# Ubuntu系统故障排查流程图

```mermaid
graph TD
    A[系统故障] --> B{能否启动?}
    B -->|能| C[进入系统排查]
    B -->|不能| D[进入恢复模式/使用Live CD]
    
    C --> E{资源问题?}
    E -->|CPU| F[使用top/htop检查]
    E -->|内存| G[使用free/vmstat检查]
    E -->|磁盘| H[使用df/du检查]
    
    C --> I{服务问题?}
    I --> J[systemctl status检查]
    I --> K[journalctl -u检查]
    
    C --> L{网络问题?}
    L --> M[ip/ifconfig检查]
    L --> N[ping/traceroute检查]
    L --> O[netstat/ss检查]
    
    C --> P{硬件问题?}
    P --> Q[dmesg检查]
    P --> R[smartctl检查]
    
    D --> S[fsck修复文件系统]
    D --> T[mount重新挂载]
    D --> U[dpkg修复包]



