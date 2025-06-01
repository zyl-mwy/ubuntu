* sudo apt install virt-manager
* sudo apt-get install -y freerdp2-x11
* sudo usermod -a -G libvirt $(whoami)
* sudo usermod -a -G kvm $(whoami)

* 创建新虚拟系统
```
本地安装介质
名称改为RPDWindows
勾选安装前自定义
CPU数那里XML删除<cpu>那里的<timer name="rtc" tickpolicy="catchup"/> 和 <timer name="pit" tickpolicy="delay"/> 删除
                          <timer name="hpet" present="no"/> 的 no 改为 yes
```


* mkdir  ~/.config/winapps
* vim ~/.config/winapps/winapps.conf
* bin/winapps check
* ./installer.sh
