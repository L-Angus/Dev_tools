# makefile tutorial

## 1. make与makefile介绍
```
makefile是一个编译指令集合的脚本文件，而make是解释makefile文件指令的命令工具。makefile最大的好处就是自动化编译，一旦写好了，只要一个make命令，整个工程就可以自动编译，极大提高开发效率。
```

利用make工具可以自动完成编译工作，这些工作包括：
1. 如果修改了某几个源文件，则只重新编译这几个文件；
2. 如果某个头文件被修改了，则重新编译所有包含该头文件的源文件；
利用这种自动编译可大大简化开发工作，避免不必要的重新编译。

make工具通过一个称为makefile的文件来完成并自动维护编译工作。makefile文件描述了整个工程的编译、链接等规则。


## 2. makefile基本规则
```c
target ...: prerequisites ...
	command
	...
	...
```
target: 可以是一个object file(目标文件)，也可以是一个执行文件，还可以是一个标签(label)。
prerequisites: 生成该target所依赖的文件和/或target。
command: 该target要执行的命令(任意的shell命令)。

```markdown
prerequisites中如果有一个以上的文件比target文件要新的话，command所定义的命令就会被执行。
```

**Demo:**
```makefile
edit: main.o hello.o
	g++ -o edit main.o hello.o

main.o: main.cpp hello.h
	g++ -c main.cpp

hello.o: hello.cpp hello.h
	g++ -c hello.cpp

clean:
	rm edit main.o hello.o
```

## 3. 简单的makefile编写
## 4. make自动化变量
## 5. makefile编译多个可执行文件
