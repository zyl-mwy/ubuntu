## 固定ip
### 方法1

* sudo nano /etc/netplan/50-cloud-init.yaml
```
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: no
      addresses: [192.168.10.2/24]
```

```
network:
  version: 2
  ethernets:
    eth0:
      dhcp4: yes  # 开启DHCP
      dhcp4-overrides:
        route-metric: 100  # 设置路由优先级（数字越小优先级越高）
      addresses: [192.168.10.2/24]  # 同时设置静态IP
      dhcp4: false  # 实际使用静态IP，这行会覆盖上面的dhcp4: yes
      
  wifis:
    wlan0:
      optional: true
      dhcp4: true
      dhcp4-overrides:
        route-metric: 200  # WiFi优先级较低
      regulatory-domain: "CN"
      access-points:
        "linxi":
          hidden: true
          auth:
            key-management: "psk"
            password: "489da4c177223ab9c12b8141c739f3836e114525dd712b0ad0cae53224865e70"
```
* sudo netplan apply
* ip addr


### 方法2
#### 固定ip
* nmcli con show

* sudo nmcli con mod "Wired connection 1" ipv4.addresses "192.168.10.2/24"
* sudo nmcli con mod "Wired connection 1" ipv4.gateway "192.168.10.1"
* sudo nmcli con mod "Wired connection 1" ipv4.method manual

* sudo nmcli con mod "Wired connection 1" ipv4.dns "8.8.8.8 8.8.4.4"
* sudo nmcli con mod "Wired connection 1" ipv6.method ignore

* sudo nmcli con down "Wired connection 1" && sudo nmcli con up "Wired connection 1"

* ip a
* ip r

#### 解除固定ip
* sudo nmcli con mod "Wired connection 1" ipv4.method auto
* sudo nmcli con mod "Wired connection 1" ipv4.gateway ""
* sudo nmcli con mod "Wired connection 1" ipv4.addresses ""
* sudo nmcli con mod "Wired connection 1" ipv4.dns ""
* sudo nmcli con down "Wired connection 1"
* sudo nmcli con up "Wired connection 1"

## 设定mtu
* sudo ip link set dev eth0 down
* sudo ip link set dev eth0 mtu 2500
* sudo ip link set dev eth0 up
* ip link show eth0 | grep mtu
