# 使用技巧
## 进程管理
* ps -ef | grep docker
* ps -ef | grep docker | awk '{print $2}'
* kill -15 ID 发送终止信号
* kill -9 ID 强制终止
* pkill ID
