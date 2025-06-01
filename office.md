* sudo apt install virt-manager
* sudo apt-get install -y freerdp2-x11
* sudo usermod -a -G libvirt $(whoami)
* sudo usermod -a -G kvm $(whoami)

* 创建新虚拟系统
```
本地安装介质
名称改为RPDWindows
勾选安装前自定义
```


* mkdir  ~/.config/winapps
* vim ~/.config/winapps/winapps.conf
* bin/winapps check
* ./installer.sh
