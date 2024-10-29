# 选择语句

## 1. if()else选择语句

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

· C99 · 

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