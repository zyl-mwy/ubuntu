* 规则举例
```
foo.o : foo.c defs.h # foo模块
	cc -c -g foo.c
```

* 规则的语法
```
targets : prerequisites
    command
    ...
```

```
targets : prerequisites ; command
    command
    ...
```

* 在规则中使用通配符
```
clean:
rm -f *.o
```

```
print: *.c
    lpr -p $?
    touch print
```

```
objects = *.o
```

```
objects := $(wildcard *.o)
```

* 文件搜寻
```
VPATH = src:../headers
```

```
vpath <pattern> <directories>
为符合模式<pattern>的文件指定搜索文件夹<directories>。

vpath <pattern>
清除符合模式<pattern>的文件的搜索文件夹。

vpath
清除全部已被设置好了的文件搜索文件夹。
```

```
vpath %.h ../headers
```

```
vpath %.c foo
vpath % blish
vpath %.c bar
```

```
vpath %.c foo:bar
vpath % blish
```

* 伪目标
```
clean:
	rm *.o temp
```


