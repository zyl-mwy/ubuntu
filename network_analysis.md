# wireshark
## install and run
* sudo apt install wireshark
* sudo wireshark
## structure
* 物理层-数据链路层-网络层-传输层-应用层
## filter
### 显示过滤器
* ip.addr == 192.168.44.1 && HTTP && tcp.port == 80 
* 作为过滤器应用 且选中
* 作为过滤器应用 选中 将“==”改为“contains”
* http2
### 捕获过滤器

## practice
### 基本
* arp
```
设备到路由器互相知道mac和ip
```
* dns
```
域名到ip
```

### tcp协议
#### http
* 过滤器条件
```
ip.addr == 52.58.199.22 or ip.addr == 3.125.197.172
```
* bash命令
```
curl http://nginx.org/LICENSE
```
* 结果
```
建链接三次握手
数据传输
断链接四次握手
```

#### https
* 过滤器条件
```
ip.addr == 52.58.199.22 or ip.addr == 3.125.197.172 and tls
```
* bash命令
```
curl https://nginx.org/LICENSE
```


