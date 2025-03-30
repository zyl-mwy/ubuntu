## 显示当前目录
* pwd

## 列出目录内容
* ls
* ls -l    # 显示详细信息
* ls -a    # 显示隐藏文件

## 切换目录
* cd /path/to/directory

## 创建目录
* mkdir new_directory

## 删除文件或目录
* rm file_name
* rm -r directory_name  # 删除目录及其内容

## 复制文件或目录
* cp source_file target_file
* cp -r source_directory target_directory

## 移动或重命名文件
* mv source_file target_file
* mv old_name new_name

## 查看文件内容
* cat file_name
* less file_name
* more file_name

## 按行查看文件内容
* head -n 10 file_name  # 查看前 10 行
* tail -n 10 file_name  # 查看后 10 行

## 清空终端
* clear

## 查找文件
* find /path -name file_name

## 搜索文本内容
* grep "text" file_name
* grep -r "text" directory_name  # 递归搜索

## 创建符号链接
* ln -s target_file link_name
