* 显示命令
```
@echo 正在编译XXX模块......
```

* 命令运行
```
exec:
    cd /home/hchen
    pwd
```

```
exec:
	cd /home/hchen; pwd
```

* 命令出错
```
clean:
	-rm -f *.o
```

* 嵌套运行make
```
subsystem:
	cd subdir && $(MAKE)
```
等效于：
```
subsystem:
	$(MAKE) -C subdir
```
