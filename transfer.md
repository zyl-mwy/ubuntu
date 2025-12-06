## 单纯传输文件

* scp XXX.doc nvidia@172.23.100.201:~

### 报错修复
#### 从电脑到树莓派
* ssh-keygen -f "/home/linxi-ice/.ssh/known_hosts" -R "192.168.10.2"
#### 从树莓派到电脑
* sudo apt install openssh-server  # 如果未安装
* sudo systemctl start ssh
* sudo systemctl enable ssh
* sudo systemctl status ssh
* sudo netstat -tlnp | grep ssh




## 完整的Samba共享文件夹设置流程

### 第一步：安装Samba（如果还没安装）

```bash
# 更新软件包列表
sudo apt update

# 安装Samba
sudo apt install samba -y
```

### 第二步：创建共享目录

```bash
# 在你的主目录创建共享文件夹
mkdir ~/shared-folder

# 设置权限（允许所有人读写）
chmod 777 ~/shared-folder
```

或者如果你已经有了要共享的目录：
```bash
# 例如，共享现有的project目录
chmod -R 777 ~/shared
```

### 第三步：备份并配置Samba

```bash
# 备份原始配置文件
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.backup

# 使用默认配置文件
sudo cp /usr/share/samba/smb.conf /etc/samba/smb.conf
```

### 第四步：编辑Samba配置文件

```bash
sudo nano /etc/samba/smb.conf
```

或者使用 `sudo vim /etc/samba/smb.conf`

在文件末尾添加以下内容：

```ini
# 共享配置开始
[shared]
    # 共享的目录路径（修改为你的实际路径）
    path = /home/linxi-ice/shared
    
    # 允许在网络上浏览
    browseable = yes
    
    # 可写权限
    writable = yes
    
    # 允许访客访问（不需要密码）
    guest ok = yes
    
    # 不是只读
    read only = no
    
    # 文件创建权限
    create mask = 0777
    
    # 目录创建权限
    directory mask = 0777
    
    # 强制使用你的用户名（可选）
    force user = linxi-ice
    
    # 强制使用你的用户组（可选）
    force group = linxi-ice
```

**保存并退出：**
- Nano: `Ctrl+X` → `Y` → `Enter`
- Vim: `:wq` → `Enter`

### 第五步：测试配置语法

```bash
# 测试配置文件语法
sudo testparm
```

如果看到类似这样的输出，说明配置正确：
```
Load smb config files from /etc/samba/smb.conf
Processing section "[shared]"
Loaded services file OK.
```

### 第六步：重启Samba服务

```bash
# 重启Samba服务
sudo systemctl restart smbd

# 重启NetBIOS服务（可选）
sudo systemctl restart nmbd

# 设置开机自启
sudo systemctl enable smbd
```

### 第七步：检查服务状态

```bash
# 查看服务状态
sudo systemctl status smbd --no-pager
```

应该看到绿色的 `active (running)` 状态。

### 第八步：测试本地访问

```bash
# 测试本地访问
smbclient -L localhost
```

或者查看共享：
```bash
# 列出共享
smbclient //localhost/shared -U%
```

### 第九步：获取IP地址

```bash
# 查看本机IP地址
ip addr show

# 或使用更简洁的方式
hostname -I
```

你会看到类似 `192.168.1.100` 的IP地址，记下来。

### 第十步：从其他设备访问

#### 从其他Linux电脑访问：
1. 打开文件管理器
2. 点击"其他位置"
3. 在"连接到服务器"输入：`smb://你的IP地址`
   - 例如：`smb://192.168.1.100`
4. 双击 `shared` 文件夹即可访问

#### 从Windows电脑访问：
1. 打开文件资源管理器
2. 在地址栏输入：`\\你的IP地址`
   - 例如：`\\192.168.1.100`
3. 按回车，双击 `shared` 文件夹

#### 从macOS访问：
1. 打开Finder
2. 菜单栏选择"前往" → "连接服务器"
3. 输入：`smb://你的IP地址`
4. 点击"连接"

### 第十一步：创建带密码保护的共享（可选）

如果你需要密码保护：

```bash
# 1. 修改配置文件
sudo nano /etc/samba/smb.conf
```

修改 `[shared]` 部分：
```ini
[shared]
    path = /home/linxi-ice/shared
    browsable = yes
    writable = yes
    guest ok = no  # 改为no，需要密码
    read only = no
    valid users = linxi-ice
```

```bash
# 2. 添加Samba用户密码
sudo smbpasswd -a linxi-ice
# 输入并确认密码

# 3. 重启服务
sudo systemctl restart smbd
```

### 第十二步：防火墙设置（如果需要）

```bash
# 允许Samba通过防火墙
sudo ufw allow samba

# 或者手动开放端口
sudo ufw allow 139/tcp
sudo ufw allow 445/tcp
sudo ufw allow 137/udp
sudo ufw allow 138/udp
```

### 故障排除

如果遇到问题：

1. **检查服务状态**：
```bash
sudo systemctl status smbd -l --no-pager
```

2. **查看错误日志**：
```bash
sudo tail -50 /var/log/samba/log.smbd
```

3. **检查目录权限**：
```bash
ls -ld ~/shared
# 应该显示 drwxrwxrwx 权限
```

4. **重新测试配置**：
```bash
# 测试配置
sudo testparm

# 如果配置错误，恢复备份
sudo cp /etc/samba/smb.conf.backup /etc/samba/smb.conf
```

### 快速脚本（一键配置）

保存为 `setup-samba.sh`，然后 `chmod +x setup-samba.sh` 并运行：

```bash
#!/bin/bash
echo "=== Samba共享文件夹一键配置 ==="

# 创建共享目录
echo "1. 创建共享目录..."
mkdir -p ~/shared-folder
chmod 777 ~/shared-folder

# 备份并创建配置
echo "2. 配置Samba..."
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.backup
sudo cp /usr/share/samba/smb.conf /etc/samba/

# 添加共享配置
echo "3. 添加共享设置..."
cat << EOF | sudo tee -a /etc/samba/smb.conf

[shared]
    path = /home/$(whoami)/shared-folder
    browsable = yes
    writable = yes
    guest ok = yes
    read only = no
    create mask = 0777
    directory mask = 0777
EOF

# 重启服务
echo "4. 重启服务..."
sudo systemctl restart smbd
sudo systemctl restart nmbd

# 显示状态
echo "5. 检查状态..."
sudo systemctl status smbd --no-pager | head -20

# 显示IP地址
echo -e "\n=== 配置完成 ==="
echo "共享路径: /home/$(whoami)/shared-folder"
echo "本地IP地址: $(hostname -I | awk '{print $1}')"
echo "访问方式: smb://$(hostname -I | awk '{print $1}')"
echo "或: \\\\$(hostname -I | awk '{print $1}') (Windows)"
```

这样就完成了！你的共享文件夹应该可以通过局域网访问了。
