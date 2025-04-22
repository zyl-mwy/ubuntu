mkdir -p /etc/apt/keyrings

wget -qO - https://apt.v2raya.org/key/public-key.asc | sudo tee /etc/apt/keyrings/v2raya.asc

echo "deb [signed-by=/etc/apt/keyrings/v2raya.asc] https://apt.v2raya.org/ v2raya main" | sudo tee /etc/apt/sources.list.d/v2raya.list

sudo apt update

sudo apt install v2raya v2ray

sudo v2raya --reset-password #重置密码

sudo systemctl start v2raya.service

sudo systemctl enable v2raya.service

http://127.0.0.1:2017/

透明代理/系统代理：启用大陆白名单模式

透明代理/系统代理实现方式：redirect

规则端口的分流模式：大陆白名单模式

防止DNS污染：关闭

特殊模式：关闭

TCPFastOpen：保持系统默认

嗅探：Http+TLS+Quic

多路复用：关闭

自动更新订阅：服务器启动时更新订阅

解析订阅链接/更新时优先使用：跟随透明代理/系统代理






