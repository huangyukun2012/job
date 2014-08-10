一、语法
二、语言运行原理
一、语法
1.const 
Q:函数形参列表之后，大括号之前的const表示什么意义？
Q:函数重载要求函数具有不同的函数签名，函数签名包括哪些部分？分析下列函数签名，哪些是相同的？
class ClassName{
	int function(int a, int b);
	double function(int a, int b) const;
	const int function(int a, int b);
	int function(int a, int b) const;
}

2.类型转化
C++中有几种类型转化？分别是什么？有何区别？

3.

二、语言运行原理
1.C++中，main函数之前执行的工作有哪些？程序的入口是什么？

我们看下面的例子：
　　　　
　　　　/* file name test00.c */
　　　　
　　　　int main(int argc, char* argv)
　　　　{
　　　　 return 0;
　　　　}
　　　　
　　　　编译链接它：
　　　　cc test00.c -o test.exe
　　　　会生成 test.exe
　　　　
　　　　但是我们加上这个选项： -nostdlib (不链接标准库)
　　　　cc test00.c -nostdlib -o test.exe
　　　　链接器会报错：
　　　　undefined symbol: __start
　　　　
　　　　也就是说：
　　　　1. 编译器缺省是找 __start 符号，而不是 main
　　　　2. __start 这个符号是程序的起始点
　　　　3. main 是被标准库调用的一个符号
通常，我们会在编译器的环境中找到一个名字类似于 crt0.o 的文件，这个文件中包含了我们刚才所说的 __start 符号。

那么真正的 crt0.s 是什么样子呢？下面我们给出部分伪代码：
　　　　
　　　　///////////////////////////////////////////////////////
　　　　section .text:
　　　　__start:
　　　　
　　　　 :
　　　　 init stack;
　　　　 init heap;
　　　　 open stdin;
　　　　 open stdout;
　　　　 open stderr;
　　　　 :
　　　　 push argv;
　　　　 push argc;
　　　　 call _main; (调用 main)
　　　　 :
　　　　 destory heap;
　　　　 close stdin;
　　　　 close stdout;
　　　　 close stderr;
　　　　 :
　　　　 call __exit;
　　　　////////////////////////////////////////////////////

总结：
main函数执行之前，主要就是初始化系统相关资源：
1.设置栈指针
2.初始化static静态和global全局变量，即data段的内容
3.将未初始化部分的赋初值：数值型short，int，long等为0，bool为FALSE，指针为NULL，等等，即.bss段的内容
4.运行全局构造器，估计是C++中构造函数之类的吧
5.将main函数的参数，argc，argv等传递给main函数，然后才真正运行main函数

