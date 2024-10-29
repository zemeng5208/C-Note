# 循环语句

## 1.跳转语句

#### 1. break 语句

break 语句只能用于循环体内或 switch 语句内，并且会使得程序流跳转到该循环或该 switch 语句后面的第一条语句。break 语句的语法如下：

```c
break;
```

因此，无论在循环体内什么位置，break 语句都可以造成循环的结束。

#### 2.continue 语句

continue 语句只能在循环体内使用，并且会造成程序流跳过当前循环中尚未执行的代码部分。它的语法如下：

```c
continue;
```

在 while 或 do…while 循环中，当遇到 continue 语句时，程序会跳转到循环的控制表达式，并进行下一次的循环条件计算。在 for 循环中，程序会跳转到循环头部的第三个表达式，并进行下一次的循环条件计算。

#### 3.goto 语句

goto 语句会造成无条件跳转，它跳转到同一个函数中的另一条语句。跳转的目的地使用标签名称来指定，语法如下：

```c
goto 标签名称;
```

标签有自己的命名空间，也就是说，标签可以使用与变量或类型一样的名称，而不会发生冲突。标签可以被放在任何语句的前面，并且一条语句也可以有多个标签。标签的目的是标识 goto 语句的目的地，对于语句本身，没有任何影响，被贴上标签的语句依然可以由上而下顺序地执行。

#### 4.return 语句



## 2.while()循环语句

#### 1. while 的基本用法

while 的基本格式如下：

```
while(控制表达式){
    循环体
}
```

> 执行 while 语句时，首先计算控制表达式的值。如果值不为零，那么执行循环体，接着再次判定 控制表达式的真值，如果为真，再次执行循环体。直到控制表达式的真值为假，才会结束 while 语句。

```c
#include <stdio.h>
int main(){
    char ch;
    while ((ch = getchar()) != '\n')
    {
      putchar(ch);
    }   
    return 0;
}
```

上述代码为while语句解决字符串输出空格的一个案例

- **while 循环终止时，控制表达式的值一定为假**。

  ```
  int i = 10;
  while(i > 0){
      printf("%d\n", i);
      i--;
  }
  printf("%d", i); // i is now 0
  ```

- **可能根本不执行 while 循环体**。

  ```
  int i = 0;
  while(i > 0){
      printf("%d\n", i);
      i--;
  }
  // Nothing is printed.
  ```

- **while 语句常有多种写法**

  ```
  int i = 10;
  while(i > 0){
      printf("%d\n", i--); // 将 i-- 写在 printf 内，简化循环
  }
  ```

#### 2. 无限循环

> 如果控制表达式的值始终非零，while 循环将无法终止。

```
while(1){
    printf("Hello World\n");
}
```

除非循环体内有控制循环的语句（break，return，goto）或者调用了导致程序终止的函数，非则上面的循环永远不会结束。

斐波那契数列：

```c
#include <stdio.h>
int main()
{
    int n, i = 1, j = 1, k, count = 2;
    printf("请输入要计算的斐波那契数列的长度：");
    scanf("%d", &n);
    printf("斐波那契数列的前%d个数为：", n);
    printf("%d %d ", i, j);
    while (count < n)
    {
        k = i + j;
        printf("%d ", k);
        i = j;
        j = k;
        count++;
    }
    printf("\n");
    return 0;
}
```

