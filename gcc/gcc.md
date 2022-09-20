# 入门gcc
## 1. 什么是gcc？
gcc（GNU C Compiler）编译器的作者是Richard Stallman，也是GNU项目的奠基者。
gcc是GNU Compiler Collection的缩写，最初是C语言的编译器，现在支持多种语言，C++、java等。
gcc支持多种硬件平台。
## 2. gcc的主要特征？
gcc是一个可移植的编译器，支持多种硬件平台；
gcc不仅仅是个本地编译器，它还能跨平台交叉编译。
gcc有多种语言前端，用于解析不同的语言；
gcc是按模块设计的，可以加入新语言和新的CPU架构的支持；
gcc是自由软件。
## 3. gcc的编译过程？
hello.c--->hello.i--->hello.s--->hello.o--->hello；
gcc编译器通过预处理器将hello.c源程序预处理为hello.i文件（被修改的源程序）；然后通过编译器将hello.i文件编译成汇编程序hello.s；再通过汇编器将hello.s程序处理成hello.o程序；最后通过链接器生成可执行程序hello，并以二进制的格式存储在磁盘中，当需要执行程序时，CPU将其读入到内存中执行。
## 4. gcc的常用选项？
-o: 生成目标文件（.i,.s,.o,可执行文件等）；
-c: 通知gcc取消链接步骤，即编译源码并在最后生成目标文件；
-E: 只运行C预编译器；
-S: 告诉编译器产生汇编语言文件后停止编译，产生的汇编语言文件扩展为.s；
-Wall: 使gcc对源文件的代码有问题的地方发出警告；
-Idir: 将dir目录加入搜索头文件的目录路径；
-Ldir: 将dir目录加入搜索库的目录路径；
-llib: 链接lib库；
-g: 在目标文件中嵌入调试信息，以便gdb之类的调试程序调试。
```c
gcc -E hello.c -o hello.i(预处理)
gcc -S hello.i -o hello.s(编译)
gcc -c hello.s -o hello.o(汇编)
gcc hello.o -o hello(链接)
---------------------------------
gcc hello.c -o hello(直接编译链接生成可执行目标文件)
```
## 5. gcc编译多文件
```c
gcc hello.c main.c -o hello
```
==头文件不参与gcc编译。==

## 6. 头文件与库文件
好处：
1. 模块化
2. 可重复性高
3. 可维护性好

## 7. 静态库和共享库
### 静态库
程序在编译链接的时候把库的代码链接到可执行文件中，程序运行的时候将不再需要静态库。
### 共享库
程序在运行的时候才去链接共享库的代码，多个程序共享使用库的代码。
共享库可以在多个程序间共用，所以动态链接使得可执行文件更小，节省了磁盘空间。由于操作系统采用虚拟内存机制，使得物理内存中所有进程都共用同一份共享库，节省了内存空间。
### 生成静态库
```c
gcc -c -Wall hello.c -o hello.o
ar rcs libhello.a hello.o // ar是gnu归档工具，rcs表示replace and create；
gcc -Wall main.c libhello.a -o main
gcc -Wall -L. main.c -o main -lhello // -L.表示在当前目录下搜索库文件
```
### 生成共享库
gcc -c hello.c -o hello.o
gcc -shared -fPIC hello.o -o libhello.so
gcc -Wall -L. main.o -o main -lhello


