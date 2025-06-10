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
