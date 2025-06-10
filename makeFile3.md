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

```
export <variable ...>
```

```
unexport <variable ...>
```

```
export variable = value
```
等效于：
```
variable = value
export variable
```
等效于：
```
export variable := value
```
等效于：
```
variable := value
export variable
```

```
export variable += value
```
等效于：
```
variable += value
export variable
```

```
subsystem:
	cd subdir && $(MAKE) MAKEFLAGS=
```

* 定义命令包
```
define run-yacc
yacc $(firstword $^)
mv y.tab.c $@
endef
```

```
foo.c : foo.y
	$(run-yacc)
```

* 变量的基础
```
objects = program.o foo.o utils.o
program : $(objects)
	cc -o program $(objects)

$(objects) : defs.h
```

```
foo = c
prog.o : prog.$(foo)
$(foo)$(foo) -$(foo) prog.$(foo)
```

```
prog.o : prog.c
	cc -c prog.c
```
