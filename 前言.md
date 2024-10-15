# C语言

## 前言

这是一个大学生的学习笔记，对引入的资料并没有侵犯只是版权的意思，只是用于学习交流

## 一.第一个c语言程序

```c
#include <stdio.h>

int main()
{
    for (int i = 0; i < 100; i++)
        printf("Hello~%d\n", i); 

    return 0;
}
```

介绍：引入头文件库，写出main函数，并且调用printf函数来打印hello~，

当然，main函数推荐这样写

```c
#include<stdio.h>

int main(void){
    
    printf("Hello，World\n");//a simple C program
    
    return 0;
}
```

集成开发环境

> 集成开发环境（`integrated development enviroment,IDE`）：集成开发环境是一个软件包，我们可以在其中编辑，编译，链接，执行和调试程序。

### 1. 指令

示例程序第一行`#include<stdio.h>`就是一条指令。

在程序**编译之前**，C编译器的**预处理器**（preprocessor）会首先对源代码进行一些准备工作，即预处理（preprocessing）。

> **指令(directive)：**我们把 预处理器 执行的命令称为 预处理器指令（preprocessor directive），简称指令。
>
> 指令的结尾不需要添加分号

`#include<stdio.h>`的作用相当于把 **头文件** `stdio.h` 中的所有内容都输入到该行所在的位置。

实际上，这是一种**复制+粘贴**的操作。

**include 文件提供了一种方便的途径共享许多程序共有的信息**。

`stdio.h`文件中包含了供编译器使用的输入和输出函数（如 `printf()`）信息。

该文件名的含义为**标准输入/输出**头文件（`stadard input&output .header`）

> **头文件(header):**在C程序顶部的信息集合。

每个头文件都包含一些标准库的内容。

示例程序引入`stdio.h`头文件的原因：C语言不同于其他编程语言，它没有内置的“读/写”命令。输入/输出功能由标准库中的函数实现。[2](https://github.com/hairrrrr/C-CrashCourse/blob/master/content/c-mordern-approch/02-C语言基本概念.md#user-content-fn-1-cea3bb9e72771ab4d20eeb1924e89f82)

**每次用到库函数，必须用#include指令包含相关的头文件。**省略必要的头文件可能不会对某一个特定程序造成影响，但是最好不要这样做。

### 2.函数 

> **函数：**类似于其他编程语言的“过程”或“子例程”，它们是用来构建程序的构建块。

函数分两大类：第一种是程序员自己编写的函数；另一类则是C作为语言实现的一部分提供的函数，即**库函数**（library function）。因为它们属于一个由编译器提供的函数“库”。

**main函数**：C程序都是从`main()`函数“开始”执行。`main()`函数是程序的唯一入口。**可以理解为程序是从main函数开始运行到main函数结尾结束。**

**返回类型**：`int`是main函数的 返回类型。这表明 main函数返回的值是整型。

> **正确的形式**：`int main(int argc, char* argv[])`
>
> **可以接受的形式：**`int main(void)`
>
> **错误的写法**：`int main()`

### 3.注释

有两种注释方法，第一种用于单行注释：

```c
// 这是一段被注释的代码
```

第二种多用于多行注释：

```c
/* 
这是被注释的第一行
这是被注释的第二行文件
*/
```

### 4.语句

**C语言中的六种语句**

1. **标号语句**

   1. [goto](https://zh.cppreference.com/w/c/language/goto) 语句的目标。 （*标识符* **:** *语句*）
   2. [switch](https://zh.cppreference.com/w/c/language/switch) 语句的 `case` 标号。（**case** *常量表达式* **:** *语句*）
   3. [switch](https://zh.cppreference.com/w/c/language/switch) 语句的默认标号。 （**default** **:** *语句*）

2. **复合语句**

   复合语句，或称**块**，是**花括号**所包围的语句与声明的序列。

   `{声明（可选）| 语句 }`

3. **表达式语句**

   典型的 C 程序中大多数语句是表达式语句，例如赋值或函数调用。

   无表达式的表达式语句被称作*空语句*。它通常用于提供空循环体给 [for](https://zh.cppreference.com/w/c/language/for) 或 [while](https://zh.cppreference.com/w/c/language/while) 循环。

4. **选择语句**

   选择语句根据表达式的值，选择数条语句之一执行。

   1. [if](https://zh.cppreference.com/w/c/language/if) 语句
   2. [if](https://zh.cppreference.com/w/c/language/if) 语句带 `else` 子句
   3. [switch](https://zh.cppreference.com/w/c/language/switch) 语句

5. **迭代语句**

   迭代语句重复执行一条语句。

   1. [while](https://zh.cppreference.com/w/c/language/while) 循环
   2. [do-while](https://zh.cppreference.com/w/c/language/do) 循环
   3. [for](https://zh.cppreference.com/w/c/language/for) 循环

6. **跳转语句**

   跳转语句无条件地转移控制流。

   1. [break](https://zh.cppreference.com/w/c/language/break) 语句
   2. [continue](https://zh.cppreference.com/w/c/language/continue) 语句
   3. [return](https://zh.cppreference.com/w/c/language/return) 语句带可选的表达式
   4. [goto](https://zh.cppreference.com/w/c/language/goto) 语句

