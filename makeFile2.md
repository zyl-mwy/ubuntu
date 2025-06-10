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

```
.PHONY: clean
clean:
	rm *.o temp
```

```
all : prog1 prog2 prog3
.PHONY : all

prog1 : prog1.o utils.o
	cc -o prog1 prog1.o utils.o

prog2 : prog2.o
	cc -o prog2 prog2.o

prog3 : prog3.o sort.o utils.o
	cc -o prog3 prog3.o sort.o utils.o
```

```
.PHONY: cleanall cleanobj cleandiff

cleanall : cleanobj cleandiff
	rm program

cleanobj :
	rm *.o

cleandiff :
	rm *.diff
```

* 多目标
```
bigoutput littleoutput : text.g
generate text.g -$(subst output,,$@) > $@
```
上述规则等效于：
```
bigoutput : text.g
	generate text.g -big > bigoutput
littleoutput : text.g
	generate text.g -little > littleoutput
```

* 静态模式
```
objects = foo.o bar.o

all: $(objects)

$(objects): %.o: %.c
	$(CC) -c $(CFLAGS) $< -o $@
```
等价于
```
foo.o : foo.c
	$(CC) -c $(CFLAGS) foo.c -o foo.o
bar.o : bar.c
	$(CC) -c $(CFLAGS) bar.c -o bar.o
```

```
files = foo.elc bar.o lose.o

$(filter %.o,$(files)): %.o: %.c
	$(CC) -c $(CFLAGS) $< -o $@
$(filter %.elc,$(files)): %.elc: %.el
	emacs -f batch-byte-compile $<
```

* 自己主动生成依赖性
```
%.d: %.c
	@set -e; rm -f $@; \
    $(CC) -M $(CPPFLAGS) $< > $@.$$$$; \
    sed 's,/($*/)/.o[ :]*,/1.o $@ : ,g' < $@.$$$$ > $@; \
    rm -f $@.$$$$
```



