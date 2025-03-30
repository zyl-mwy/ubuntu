# 查看文件权限
ls -l

# 修改文件权限
chmod 755 file_name  # 设置权限为 rwxr-xr-x
chmod u+x file_name  # 给文件所有者添加执行权限

# 修改文件所有者
chown user_name file_name
chown user_name:group_name file_name
