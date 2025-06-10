* 使用条件推断
```
libs_for_gcc = -lgnu
normal_libs =

foo: $(objects)
    ifeq ($(CC),gcc)
    	$(CC) -o foo $(objects) $(libs_for_gcc)
    else
    	$(CC) -o foo $(objects) $(normal_libs)
    endif
```

```
libs_for_gcc = -lgnu
normal_libs =

ifeq ($(CC),gcc)
	libs=$(libs_for_gcc)
else
	libs=$(normal_libs)
endif

foo: $(objects)
$(CC) -o foo $(objects) $(libs)
```

* 语法
```
<conditional-directive>
	<text-if-true>	# 此处的缩进没有关系
endif
```

```
<conditional-directive>
	<text-if-true>
else
	<text-if-false>
endif
```

```
ifeq (<arg1>, <arg2> )
ifeq '<arg1>' '<arg2>'
ifeq "<arg1>" "<arg2>"
ifeq "<arg1>" '<arg2>'
ifeq '<arg1>' "<arg2>"
```

```
ifeq ($(strip $(foo)),)
	<text-if-empty>
endif
```

```
ifneq (<arg1>, <arg2> )
ifneq '<arg1>' '<arg2>'
ifneq "<arg1>" "<arg2>"
ifneq "<arg1>" '<arg2>'
ifneq '<arg1>' "<arg2>"
```

```
ifdef <variable-name>
```

```
bar =
foo = $(bar)
ifdef foo
	frobozz = yes
else
	frobozz = no
endif
```

```
foo =
ifdef foo
	frobozz = yes
else
	frobozz = no
endif
```

```
ifndef <variable-name>
```

* 函数的调用语法
```
$(<function> <arguments> )
```

```
$(<function> <arguments> )
```

```
comma:= ,
empty:=
space:= $(empty) $(empty)
foo:= a b c
bar:= $(subst $(space),$(comma),$(foo))
```

* 字符串处理函数
```
$(subst <from>,<to>,<text> )
```
```
$(subst ee,EE,feet on the street)
```

```
$(patsubst <pattern>,<replacement>,<text> )
```
```
$(patsubst %.c,%.o,x.c.c bar.c)
```

```
$(strip <string> )
```
```
$(strip a b c )
```

```
$(findstring <find>,<in> )
```
```
$(findstring a,a b c)
$(findstring a,b c)
```

```
$(filter <pattern...>,<text> )
```
```
sources := foo.c bar.c baz.s ugh.h
foo: $(sources)
cc $(filter %.c %.s,$(sources)) -o foo
```

```
$(filter-out <pattern...>,<text> )
```
```
objects=main1.o foo.o main2.o bar.o
mains=main1.o main2.o

$(filter-out $(mains),$(objects))
```

```
$(sort <list> )
```
