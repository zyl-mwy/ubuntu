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

* 变量中的变量
```
foo = $(bar)
bar = $(ugh)
ugh = Huh?

all:
	echo $(foo)
```

```
CFLAGS = $(include_dirs) -O
include_dirs = -Ifoo -Ibar
```

```
x := foo
y := $(x) bar
x := later
```
等效于：
```
y := foo bar
x := later
```

```
y := $(x) bar
x := foo
```

```
ifeq (0,${MAKELEVEL})
cur-dir := $(shell pwd)
whoami := $(shell whoami)
host-type := $(shell arch)
MAKE := ${MAKE} host-type=${host-type} whoami=${whoami}
endif
```

```
nullstring :=
space := $(nullstring) # end of the line
```

```
dir := /foo/bar # directory to put the frobs in
```

```
FOO ?= bar
```
等价于：
```
ifeq ($(origin FOO), undefined)
FOO = bar
endif
```

* 变量高级使用方法
```
foo := a.o b.o c.o
bar := $(foo:.o=.c)
```

```
foo := a.o b.o c.o
bar := $(foo:%.o=%.c)
```

```
x = y
y = z
a := $($(x))
```

```
x = y
y = z
z = u
a := $($($(x)))
```

```
x = $(y)
y = z
z = Hello
a := $($(x))
```

```
x = variable1
variable2 := Hello
y = $(subst 1,2,$(x))
z = y
a := $($($(z)))
```

```
first_second = Hello
a = first
b = second
all = $($a_$b)
```

```
a_objects := a.o b.o c.o
1_objects := 1.o 2.o 3.o

sources := $($(a1)_objects:.o=.c)
```
