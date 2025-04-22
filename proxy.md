mkdir -p /etc/apt/keyrings

wget -qO - https://apt.v2raya.org/key/public-key.asc | sudo tee /etc/apt/keyrings/v2raya.asc

echo "deb [signed-by=/etc/apt/keyrings/v2raya.asc] https://apt.v2raya.org/ v2raya main" | sudo tee /etc/apt/sources.list.d/v2raya.list

sudo apt update

sudo apt install v2raya v2ray

sudo v2raya --reset-password #重置密码

sudo systemctl start v2raya.service

sudo systemctl enable v2raya.service
