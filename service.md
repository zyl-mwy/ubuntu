# 服务 
## 服务基本启动和关闭
* sudo service xxx start
* sudo service xxx stop
* sudo service xxx restart
* sudo service xxx status
## 服务文件存放位置
* /lib/systemd/system/ 默认服务目录
* /etc/systemd/system/ 管理员服务目录
* /run/systemd/system/ 临时服务目录
## 查找特定服务文件的方法
* systemctl show nginx --no-pager -p FragmentPath
* sudo find /lib/systemd/system /etc/systemd/system -name "*.service" | grep mysql
* systemctl cat docker
## 服务文件示例
```
[Unit]
Description=nginx - high performance web server
After=network.target

[Service]
Type=forking
PIDFile=/run/nginx.pid
ExecStart=/usr/sbin/nginx -c /etc/nginx/nginx.conf
ExecReload=/usr/sbin/nginx -s reload
ExecStop=/usr/sbin/nginx -s stop

[Install]
WantedBy=multi-user.target
```
## 修改现有服务
* sudo systemctl edit <服务名>  # 会保存在/etc/systemd/system/<服务名>.service.d/override.conf
## 创建自定义服务
* sudo nano /etc/systemd/system/my-service.service
* sudo systemctl daemon-reload
* sudo systemctl enable --now my-service
## 删除自定义服务
* sudo rm /etc/systemd/system/my-service.service
* sudo systemctl daemon-reload
## 注意事项
* 不要直接修改 /lib/systemd/system/ 下的文件
这些文件会被 apt 包管理器覆盖，应使用 /etc/systemd/system/ 下的覆盖配置。
* 修改后必须重载 systemd, 及 sudo systemctl daemon-reload
* 检查服务依赖关系，及 systemctl list-dependencies <服务名>

