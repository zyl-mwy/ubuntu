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
* sudo netplan apply
* ip addr
