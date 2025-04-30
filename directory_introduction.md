# Ubuntu 根目录 (`/`) 文件夹作用详解

Ubuntu 的根目录遵循 **Filesystem Hierarchy Standard (FHS)** 标准，每个目录有特定用途。本文档详细说明各核心目录的作用。

## 核心目录

### `/bin`
- **作用**：存放**基本用户命令**（二进制可执行文件），如 `ls`、`cp`、`bash` 等。
- **特点**：
  - 所有用户均可使用
  - 系统启动或修复时必需

### `/boot`
- **作用**：包含**启动引导文件**：
  - `vmlinuz`（内核）
  - `initramfs`（初始内存文件系统）
  - `grub`（引导加载程序）
- **警告**：误删可能导致系统无法启动。

### `/dev`
- **作用**：**设备文件**目录，如：
  - `sda`（磁盘）
  - `tty`（终端）
  - `null`（空设备）
- **特点**：文件对应硬件或虚拟设备，由内核动态生成。

### `/etc`
- **作用**：存放**系统全局配置文件**，例如：
  - `apt/sources.list`（软件源配置）
  - `passwd`（用户账户）
  - `fstab`（文件系统挂载表）
- **重要文件**：
  - `/etc/network/interfaces`（网络配置）
  - `/etc/ssh/sshd_config`（SSH 服务配置）

### `/home`
- **作用**：**用户主目录**，每个用户拥有独立子目录（如 `/home/username`）。
- **包含内容**：
  - 个人文件
  - 用户配置（`~/.config`）
  - 桌面环境设置
- **注意**：多用户系统中最重要的数据存储位置。

### `/lib` 与 `/lib64`
- **作用**：存放**系统库文件**（`.so` 文件）。
- **区别**：
  - `/lib`：32 位系统库
  - `/lib64`：64 位系统库（在 64 位系统中）

### `/media` 与 `/mnt`
- **`/media`**：
  - 自动挂载**可移动设备**（如 U 盘、光盘）
- **`/mnt`**：
  - 临时手动挂载文件系统（如网络共享、额外磁盘）

### `/opt`
- **作用**：**可选软件包**安装目录。
- **典型用途**：
  - 第三方商业软件（如 MATLAB、Google Chrome）
- **特点**：
  - 软件的所有文件集中在一个子目录（如 `/opt/google/chrome`）

### `/proc`
- **作用**：**虚拟文件系统**，动态反映**内核和进程信息**。
- **示例文件**：
  - `/proc/cpuinfo`（CPU 信息）
  - `/proc/meminfo`（内存信息）
- **特点**：
  - 文件大小均为 0
  - 内容由内核实时生成

### `/root`
- **作用**：**超级用户（root）的主目录**。
- **注意**：
  - 不是 `/home/root`
  - 普通用户无权限访问

### `/run`
- **作用**：存放**运行时临时数据**：
  - PID 文件
  - 套接字文件
- **特点**：
  - 重启后清空
  - 替代旧版 `/var/run`

### `/sbin`
- **作用**：存放**系统管理命令**：
  - `fdisk`（磁盘分区）
  - `iptables`（防火墙）
  - `reboot`（重启）
- **注意**：通常需要 root 权限执行

### `/srv`
- **作用**：存放**服务数据**：
  - Web 服务器：`/srv/www`
  - FTP 服务：`/srv/ftp`
- **现状**：实际使用较少，更多服务数据可能放在 `/var`

### `/tmp`
- **作用**：**临时文件**目录。
- **特点**：
  - 所有用户可读写
  - 默认重启后清空（可通过 `systemd-tmpfiles` 配置）

### `/usr`
- **作用**：**用户程序与只读数据**（占用空间最大）。
- **重要子目录**：
  - `bin`：非必需的用户命令（如 `python`、`git`）
  - `lib`：程序库文件
  - `local`：本地编译安装的软件（优先级高于 `/usr`）
  - `share`：架构无关的数据（如文档、图标）
  - `src`：内核源代码（如 `/usr/src/linux-headers-*`）

### `/var`
- **作用**：**可变数据**（日志、缓存、数据库等）。
- **关键子目录**：
  - `log`：系统日志（如 `syslog`、`auth.log`）
  - `cache`：应用程序缓存（如 `apt` 的 `/var/cache/apt`）
  - `lib`：动态数据（如 Docker 的 `/var/lib/docker`）
  - `spool`：队列数据（如邮件 `/var/spool/mail`）

## 特殊目录

### `/lost+found`
- **作用**：`fsck` 工具修复文件系统时，恢复的碎片文件存放处。

### `/snap`
- **作用**：Ubuntu 特有的 Snap 包安装目录（如 `/snap/chromium`）。

## 目录对比总结

| 目录       | 主要用途                          | 是否可删除/修改       |
|------------|-----------------------------------|----------------------|
| `/bin`     | 基础命令                          | ❌ 不可删（系统崩溃） |
| `/etc`     | 配置文件                          | ⚠️ 谨慎修改          |
| `/home`    | 用户数据                          | ✅ 可删（但数据丢失） |
| `/tmp`     | 临时文件                          | ✅ 自动清理          |
| `/var/log` | 日志文件                          | ✅ 可删（但影响排错） |

## 常见问题解答

### Q: `/usr/bin` 和 `/bin` 有什么区别？
- **A**: 
  - `/bin` 包含启动必需的最小命令集
  - `/usr/bin` 包含其他用户命令

### Q: 自定义软件应该安装在哪里？
- **推荐位置**：
  - `/opt`（独立目录，适合商业软件）
  - `/usr/local`（遵循 Unix 传统）

### Q: 磁盘空间不足时应该检查哪些目录？
- **重点检查**：
  1. `/var/log`（系统日志）
  2. `/var/lib`（应用程序数据库）
  3. `/home`（用户数据）

> 掌握这些目录结构，可以帮助您更高效地管理系统和排查问题！

# Ubuntu `/sys` Directory: Purpose and Usage

In Ubuntu (and other Linux systems), the `/sys` directory is a special virtual filesystem called **sysfs**. It's a mechanism provided by the kernel to expose kernel data structures, attributes, and operations to user space, allowing users and administrators to interact with hardware and kernel modules.

---

## **Primary Functions of `/sys`**

1. **Exposes Kernel Device and Driver Information**  
   `/sys` provides a structured view of hardware devices, drivers, and kernel modules. Examples:
   - `/sys/class`: Devices categorized by type (e.g., network cards, GPUs, input devices).
   - `/sys/devices`: Physical or virtual devices mapped from the kernel device tree.
   - `/sys/bus`: Devices organized by bus type (e.g., PCI, USB, SATA).

2. **Dynamic Device and Kernel Parameter Management**  
   - Modify files in `/sys` to adjust kernel or device behavior (e.g., power management, performance settings).
   - Example: Change CPU frequency governor:
     ```bash
     echo "powersave" | sudo tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor
     ```

3. **Supports `udev` and Hotplugging**  
   - The `udev` device manager relies on `/sys` to dynamically create device nodes (e.g., `/dev/sda`).
   - When a USB device is plugged in, the kernel notifies user space via `/sys`.

4. **Unified Device Model**  
   - Standardizes interfaces for tools like `lspci` and `lsusb` to access hardware info uniformly.

---

## **Common Subdirectories**

| Directory             | Purpose                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| `/sys/block`          | Info about block devices (e.g., disks, partitions).                    |
| `/sys/class/net`      | Network interface details (e.g., `eth0`, `wlan0`).                     |
| `/sys/power`          | Power management options (e.g., suspend, resume).                      |
| `/sys/module`         | Configuration and status of loaded kernel modules.                      |
| `/sys/firmware`       | BIOS/UEFI or firmware-related data (e.g., ACPI tables).                |

---

## **Difference Between `/sys` and `/proc`**
- **`/proc`**: Focuses on processes and system runtime states (used by tools like `ps`, `top`).
- **`/sys`**: Focuses on structured hardware/driver info (mounted as **sysfs**).

---

## **Important Notes**
1. **Avoid Manual Edits**  
   Modifying files in `/sys` without understanding their purpose may cause instability.
2. **Temporary Changes**  
   Changes to `/sys` are lost after reboot (use config files for persistence).
3. **Debugging Tools**  
   Commands like `udevadm`, `lshw`, and `lsblk` rely on `/sys` for data.

For hardware queries, use tools like `lspci`, `lsusb`, or explore `/sys` directly.
