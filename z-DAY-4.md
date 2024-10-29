# 选择语句

## 1. if()else()选择语句

#### 1. if

if 语句允许程序通过测试表达式的值从两种选项中选择一种。if 语句的简单格式如下：

```
if(表达式){
    语句
}
```

也可以写成（单个语句）

```
if(表达式)
    语句;
```

执行 if 语句时，先计算圆括号内表达式的值。如果表达式的值**非零**（C语言将非零值解释为真值），那么接着执行大括号内的语句。

#### 2. else 子句

```
if(表达式)
    语句;
else 
    语句;
```

如果是**复合语句**（compound statement），需要加上花括号

**加上花括号是一种好习惯。建议不管是不是复合语句，尽量都加上花括号。**

#### 3. 嵌套的 if 语句

**例2-3**：找出 i，j，k 中的最大值，并将其保存到 max 中

```
if(i > j){
    if(i > k){
        max = i;
    }else{
        max = k;
    }
}else{
    if(j > k){
        max = j;
    }else{
        max = k;
    }
}
```

#### 4. 级联式 if 语句

> 编程时常常需要判定一系列的条件，一旦其中某个条件为真就立刻停止。

如何做到呢？

**例2-4** 程序：判断 n 是大于 0 还是 等于 0 还是小于 0

使用 if else

```
if(n < 0){
    printf("n < 0");
}else{
    if(n == 0){
        printf("n = 0");
    }
    else{
        printf("n > 0");
    }
}
```

使用 else if

```
if(n < 0){
    printf("n < 0");
}
else if(n == 0){
    printf("n == 0");
}
else{
    printf("n > 0");
}
```

这样写可以避免 if else 嵌套，从而提高了书写和理解的难易度。

**级联式 if 语句书写形式：**

```
if(表达式){
 	语句;   
}
else(表达式){
    语句;
}
else{
    语句;
}
```

#### 5. “悬空 else”问题

请看下面的程序，思考 else 与 那个 if 匹配

```
if(y != 0)
    if(x != 0)
        printf("%.2f", x / y);
else
    printf("Error: y is zero!");
```

如果此时 y = 0, x = 2 会输出什么？

如果 y = 2, x = 0 会输出什么？

虽然缩进格式按时 else 属于外层 if，但是 C 语言遵循的规则是**else 子句应该属于离它最近且还未和其他 else 匹配的 if 语句**。

所以，此例中 else 属于内层的 if 语句。为了避免这种问题，最好的办法就是**加括号**。

```
if(y != 0){
    if(x != 0)
        printf("%.2f", x / y);
}
else
    printf("Error: y is zero!");
```

#### 6. 布尔值

多年以来，C语言一直缺乏适当的布尔类型。

一种解决方法是，先声明一个 int 型变量，让后将其赋值为 0 或 1：

```
int flag;
flag = 0; // 表示 flag 为 false
...
flag = 1; // 表示 flag 为 true 
```

虽然这种方法可行，但是对于程序的可读性没有多大贡献，因为没有明确的表示 flag 的赋值只能是布尔型，并没有明确指出 0 和 1就是表示真和假。

为了使得程序更加便于理解，C89 程序员通常使用 TRUE 和 FALSE 这样的名字定义宏：

```
#define TRUE 1
#define FALSE 0
```

现在对 flag 的赋值就有了更加自然的形式：

```
flag = FALSE;
...
flag = TRUE;
```

为了判定 flag 是否为真，可以用：

```
if(flag == TRUE){
    ...
}
```

或者只写：

```
if(flag){
    ...
}
```

为了发扬这一思想，我们可以进一步定义一个用作布尔类型的宏：

```
#define BOOL int;
```

声明布尔类型变量时可以用 BOOL 替代 int

```
BOOL flag;
```

现在我们就非常清楚了：flag 不是一个普通的整型变量，而是表示布尔条件。（当然编译器还是将 flag 当作 int 类型的变量。）

`C99`中提供了` _Bool` 类型：

```
_Bool flag;
```

> `_Bool`是无符号整型。但是和一般的整形不同，`_Bool `只能被赋值为 0 或 1 。一般来说，向 _Bool 类型变量中储存非零值会导致变量赋值为 1 。

```
_Bool flag = 5;
printf("%u", flag);

// 输出：
1
```

`C99 `还提供了一个新的头文件`<stdbool.h>`，改头提供了 bool 宏，用来代表 _Bool ；还提供了 true 和 false 两个宏，分别代表 1 和 0 。于是可以写：

```
#include<stdbool.h>

bool flag;
flag = true;
...
flag = false;
```

## 2.switch()选择语句

**switch 语句常用格式：**

```
switch(控制表达式){
    case 常量表达式 : 语句
        ...
    case 常量表达式 : 语句
    default : 语句
}
```

- **控制表达式：**控制表达式只能用：`整型`，`字符型的变量`（C 语言把字符当成整数来处理），不能用`浮点数 `和 `字符串`。

- **分支标号：**每一个分支的开头都有一个标号，格式如下：

  `case 常量表达式；`

  常量表达式(constant expression): 必须是·**整数或字符型**·，不能包含**变量和函数调用**。

  5 是常量表达式，5 + 10 也是常量表达式；但是 10 + n 不是常量表达式（除非 n 是表示常量的宏）。

- **语句：**每个分支标号后可以跟任意数量的语句。不需要用花括号把这些语句括起来。每组语句的最后一条通常是 break 语句。

- **break 的作用：** 本节后面会详细讨论。

- **default 语句的作用：** 控制表达式的值和所有的标号语句都不匹配的话，会执行 default 后面的语句。（default ：默认的意思）

C 语言**不允许有重复的分支标号，但对分支的顺序没有要求**，特别是 default 分支不一定要放在最后。

case 后**只可以跟随一个常量表达式**。但是，**多个分支标号可以放置在同一组语句前面** 。如：

```
switch(grade){
    case 4:
    case 3:
    case 2: 
    case 1: printf("Passing");
        	break;
    case 0: printf("Failing");
        	break;
    default:printf("Illegal grade");
        	break;
}
```

为了节省空间，可以将拥有相同语句的分支标号放在同一行：

```
switch(grade){
    case 4: case 3: case 2:  case 1: 
        	printf("Passing");
        	break;
    case 0: printf("Failing");
        	break;
    default:printf("Illegal grade");
        	break;
}
```

switch 语句**不要求一定有 default 分支**。如果 default 不存在，而且控制表达式的值和所有的标号语句都不匹配的话，控制会直接传给 switch 语句后面的语句。

#### break 语句的作用

break 会使程序“跳出” switch 语句，继续执行 switch 后面的语句。

对控制表达式求值的时，控制会跳转到与 switch 表达式相匹配的分支标号处。分支标号只是说明 switch 内部位置的标记。在执行完分支的最后一句后，程序控制“向下跳转”到下一个分支的第一条语句上，而忽略下一个分支的分支标号。如果没有 break 语句（或者其他某种跳转语句），控制将会从一个分支继续到下一个分支。思考下面的 switch 语句：

```
switch(grade){
    case 4: printf("Excellent"); 
    case 3: printf("Good");
    case 2: printf("Average");
    case 1: printf("Poor");
    case 0: printf("Failing");
    default:printf("Illegal grade");
}
```

如果 grade 的值为 3，那么显示的信息是：

```
GoodAveragePoorFailingIllegal grade
```

**注意：**忘记 break 是编程时常见的错误。虽然有时候会故意忽略 break 以便多个分支共享代码，但是通常情况下省略 break 是因为忽略。

如果有需要，**明确指出**故意省略 break 语句是一个好主意：

```
switch(grade){
    case 4: case 3: case 2:  case 1: 
			num_passing++;
        // Fail Through 
    case 0: total_grades++;
        	break;
}
```

最然 switch 语句最后一个分支不需要 break 语句，但是通常还是会加上一个 break 语句在那里，**以防止将来增加分支时出现“丢失” break 的问题**。