* sudo apt-get update
* sudo apt-get install build-essential linux-headers-$(uname -r)

* sudo apt-cache search linux-source  # 查看可用源码版本
* sudo apt-get install linux-source-4.15.0  # 安装对应版本源码

* cd /usr/src/linux-source-4.15.0
* sudo tar -xvjf linux-source-6.8.0.tar.bz2 -C /usr/src/
* sudo make menuconfig  # 进入配置界面，直接保存退出即可
* sudo make prepare
* sudo make scripts

* vim helloworld.c
```
#include <linux/init.h>
#include <linux/module.h>

static int hello_init(void)
{
    printk(KERN_ALERT "Hello, world\n");
    return 0;
}

static void hello_exit(void)
{
    printk(KERN_ALERT "Goodbye, cruel world\n");
}

MODULE_LICENSE("GPL");
module_init(hello_init);
module_exit(hello_exit);
```

* vim Makefile
```
obj-m += helloworld.o

KDIR := /lib/modules/$(shell uname -r)/build
PWD := $(shell pwd)

all:
	make -C $(KDIR) M=$(PWD) modules

clean:
	make -C $(KDIR) M=$(PWD) clean
```

* make

* sudo insmod helloworld.ko
* lsmod | grep helloworld
* dmesg | tail  # 查看printk输出

* sudo rmmod helloworld
* dmesg | tail  # 查看卸载信息

* cp /usr/src/linux-source-4.15.0/drivers/leds/leds-gpio.c .
