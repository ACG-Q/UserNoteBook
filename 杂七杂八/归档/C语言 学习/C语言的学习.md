# C语言的基础入门学习

## 🌐你好，世界

```c
#include <stdio.h>
void main(){
    printf("你好，世界！\n")
}
```

> `main`是主函数的函数名，表示这是一个主函数。
>
> 每个程序都必须有，有且只有一个主函数。

## 🗂️常量和变量

### 常量

> 在程序执行过程中，**其值不发生改变**的量称为**常量**

#### 符号常量

> 用标示符代表一个常量。在C语言中，可以用一个标识符来表示一个常量，称之为符号常量.

符号常量在使用之前必须先定义，其一般形式为：

```c
#define 标识符 常量
```

可以这样定义常量

```c
const 类型名 标识符=常量;
```

> `#define`是一条预处理命令，(预处理命令都以“#”开头)，称为宏定义命令(在后面预处理程序中将进一步介绍)，其功能是把该标识符定位为其后的常量值。一经定义，以后在程序中所有出现该标识符的地方均代之以该常量值。
>
> > 习惯上符号常量的标识符用大写字母，变量标识符用小写字母，以示区别。

```c
#include <stdio.h>
#define PRICE 30

void main() {
    int num, total;
    num = 10;
    total = num * PRICE;
    printf("total=%d",total);
}
```

#### 整型常量

##### 整型常量的表示方法

> 整型常量就是整常数。在C语言中，使用的整常数有八进制、十六进制和十进制三种。
>
> - 十进制整常数：十进制常数没有前缀。其数码为0~9
>
> - 八进制整常数：八进制整常数必须以0开头，即以0作为八进制数的前缀。数码取为0~7。八进制数通常是无符号数，
>
> - 十六进制整常数：十六进制整常数的前缀为0X或者0x，其数码为0~9，A~F或者a~f。
>
> - 整型常数的后缀：在16字长的机器上，基本整型的长度也为16位，因此表示的数的范围也是有限定的。
>
>   |                    | 范围          |
>   | ------------------ | ------------- |
>   | 十进制无符号整常数 | 0~65535       |
>   | 十进制有符号整常数 | -32768~+32767 |
>   | 八进制无符号数     | 0~0177777     |
>   | 十六进制无符号数   | 0x0~0xffff    |
>
>   > 如果使用的数超过了上述范围，就必须用长整型数来表示。长整型数是用后缀“L”或者“l”来表示的。
>
> **在程序中是根据前缀来区分各种进制数的。**

#### 实型(浮点型)常量

> 实型也被称为浮点型。实型常量也被称为实数或者浮点数。在C语言中，实数只采用十进制。它有两种形式：十进制小数形式、指数形式。

- 十进制数形式：由数码0~9和小数点组成。

- 指数形式：由十进制数，加阶码标示“e”或”E“以及阶码(只能为整数，可以带符号)组成。

  例如：

  | 实型   | 值       |
  | ------ | -------- |
  | 2.1E5  | 2.1*10⁵  |
  | 3.7E-2 | 3.7*10ˉ² |

  > 以下不是合法的实数：
  >
  > 345(无小数点)<br>E7(阶码标志E之前无数字)<br>-5(无阶码标志)<br>53.-E2(负号位置不对)<br>2.7E(无阶码)

  **标准C允许浮点数使用后缀。后缀为”f”或“F”即表示该数为浮点数。**如，`356f`和`356.`是等价的。

#### 字符常量

字符常量是用单引号括起来的一个字符。

> 在C语言中，字符常量有以下特点：
>
> - 字符常量只能用单引号括起来，不能用双引号或者其他括号。
> - 字符常量只能是单个字符，不能是字符串。
> - 字符可以是字符集中任意字符。但数字被定义位字符型之后就不能参与数值运算。

#### 字符串常量

> 字符串常量是由一对双引号括起来的字符序号。<br>字符串常量和字符常量是不同的量。(补充：char占八位而已)

##### 字符串常量和字符常量的区别

- 字符常量有单引号括起来，字符串常量由双引号括起来。

- 字符常量智能是单个字符，字符串常量则可以包含一个或多个字符。

- 可以包一个字符串常量赋值给一个字符变量，但不能把以自字符串常量赋予一个字符变量。

- 字符常量占一个字节的内存空间。字符串常量占的内存字节数等于字符串中字节数加1，增加的一个字节中存放字符`\0`(ASCII码位0)。这个是字符串结束的标志。

  例如：

  字符串“Hello World!”在内存中所占的字节

  ![Helllo World!](https://gitee.com/acg-q/pic-go-images/raw/master//2021-02-23_14:07:12.png)


### 变量

> 在程序执行过程中，**其值可变**的量称为**变量**

> 一个变量应该有一个名字，在内存中占据一定的存储单元。变量定义必须放在变量使用之前。有一半放在函数体的开头部分。**要区分变量名和变量值是两个不同的概念。**

#### 整型变量

```c
int k = 3;
```

![变量_整型变量](https://gitee.com/acg-q/pic-go-images/raw/master//2021-02-23_09:09:40.png)

> 另外：这里的3在内存中是以二进制的形式保存的<br>**一字节byte=八位bit**
>
> 数值是以补码表示的：
>
> - 正数的补码和原码相同；
> - 负数的补码：将概述的绝对值的二进制形式按位取反后再加1
>
> 例子：求-10的补码
>
> ```
> -10的绝对值：         10
> 10的原码：            0000 1010
> 取反：                1111 0101
> 再加1，得到-10的补码： 1111 0110
> ```
>
> > 补码的第一位是符号位

##### 整型变量的分类

> 注意：这里占多少个字节跟系统和编译器规定有关！可以在编译器上自己试试看

- 基本型：类型说明符为`int`，在内存中占4个字节
- 短整型：类型说明符为`short int`或`short`。所占字节和取值范围均与基本型相同。
- 长整型：类型说明符为`long int`或`long`。在内存中占4个字节。
- 无符号型：类型说明符为`unsigned`。

##### 整型变量的定义

变量定义一般形式为：

```c
#类型说明符 变量名标识符
int a,b,c;
```

> 在书写变量定义时，应注意以下几点：
>
> - 允许在一个类型说明符后，定义多个相同类型的变量。各变量名之间用“;”号间隔。类型说明符与变量名之间至少有一个空格间隔。
> - 最后一个变量名之后必须以“;”号结尾。
> - 变量定义必须放在变量使用之前，一般放在函数体的开头部分。

##### 整型数据的溢出

> 超出了整型的范围

#### 实型变量

##### 实型变量在内存中的存放形式

实型变量一般占4个字节(32位)内存空间。按指数形式存储。

例子：实数3.14159在内存的存放实现如下

| 符号 | 小数部分 | 指数部分 |
| ---- | -------- | -------- |
| +    | .314159  | 1        |

> - 小数部分占的位(bit)数越多，数的有效数字越多，精度越高。
> - 指数部分占的位数越多，则能表示的数值范围越大。

##### 实型变量的分类

> 实型变量分为：单精度(float型)，双精度(double型)，和长双精度(long double型)三类

##### 实型变量的舍入误差

> 由于实型变量是由有限的存储单元组成的，因此能提供的有效数字总是有限的。

例如：

```c
#include <stdio.h>

void main() {
    // 1.0 / 3 * 3 =? //实型运算
    printf("%f\n", 1.0 / 3 * 3); // 1.0 / 3 = 取小数(0.33333……) = 0.33333……  0.33333…… * 3 = 取小数(1) = 1.00
    // 1 / 3 * 3 = ? //整型运算
    printf("%d\n", 1 / 3 * 3); // 1 / 3 = 取整(0.33333……) = 0 0 * 3 = 取整(0) = 0
    printf("%f", 1 / 3 * 3); // 1 / 3 = 取整(0.33333……) = 0 0 * 3 = 取小数(0) = 0.00
}
/////运行结果////
// 1.000000  //
// 0         //
// 0.000000  //
///////////////
```

#### 字符变量

字符变量用来存储字符常量，即单个字符。

字符变量的类型说明符是`char`。字符变量类型定义的格式和书写规则都与整型变量相同。例如：

```c
char a,b;
```

##### 转义字符

转义字符是一种特殊的字符常量。转义字符以反斜号`\`开头，后跟一个或几个字符。转义字符具有特定的含义，不同于字符原有的意义。故称**转义**字符。

#### 字符串变量

在 C 语言中，字符串实际上是使用`null`字符` \0 `终止的一维字符数组。

```c
char a[] ='hello world!';
```

### 各类数值类型之间的混合运算

变量的数据类型是可以转换的。转换的方法有两种，一种是自动转换，一种是强制转换。自动转换发生在不同数据类型的量混合运算时，由编辑系统自动完成。自动转换遵循以下规则：

- 若参与运算量的类型不同，则先转换成同一类型，然后进行运算。
- 转换按数据长度增加的方向进行，以保证精度不降低。如果int型和long型运算时，先把int量转成long型后再进行运算。
- 所有的浮点运算都是以双精度进行的，即使仅含float单精度量运算的表达式，也要先转换成double型，再作运算。
- char型和short型参与运算时，必须先转换成int型。
- 在赋值运算中，赋值号`=`两边量的数据类型不同时，赋值号右边量的类型将转换成左边量的类型，如果右边量的数据类型长于左边长时，将丢失一部分数据，这样会降低精度，丢失的部分按四舍五入向前舍入。

![image-20210223144303271](https://gitee.com/acg-q/pic-go-images/raw/master//2021-02-23_14:43:14.png)

## 🧮数据运算

### 算术运算符和算术表达式

#### 基本的算术运算符

- 加法运算符`+`：加法运算符为双目运算符，即应有两个量参与加法运算。具有右结合性。
- 减法运算符`-`：减法运算符为双目运算符，但`-`也可作负值运算符，此为单目运算，具有左结合性。
- 乘法运算符`*`：乘法运算符为双目运算符，具有左结合性。
- 除法运算符`/`：除法运算符为双目运算符，具有左结合性。参与运算量均为整型时，结果也为整型，舍去小数，如果参与运算量中有一个是实型(浮点型)，则结果为双精度实型。
- 求模(取余)`%`

### 运算符的优先级

C语言中，运算符的运算优先级共分为15级，1级最高，15级最低。优先级高的先于优先级低的进行运算。

### 运算符的结合性

C语言中运算符的结合性分为两种，即左结合性(自左至右)和右结合性(自右至左)。

### 强制类型转换运算符

一般形式为：

```c
(类型说明符) (表达式)
```

把表达式的运算结果强制转换成类型说明符所表示的类型。

### 自增、自减运算符

- 自增`++`
- 自减`--`

有以下几种形式：

| 运用形式 | 意义            |
| -------- | --------------- |
| `++i`    | `i`先自增后运算 |
| `--i`    | `i`先自减后运算 |
| `i++`    | `i`先运算后自增 |
| `i--`    | `i`先运算后自减 |

> 注意：最容易出错的是`i++`和`i--`。特别是当它们出现在较为复杂的表达式或语句中时，常常难于弄清，因此应仔细分析。

#### 很别扭的一道题

```c
#include <stdio.h>

void main(){
    int j=5,q;
	q=(++j)+(++j)+(++j);
    printf("%d\n",q);
}
//运行结果//
// 22    //
///////////
```

> 优先级拆分：
>
> 括号`()` >>> 加号`+` >>> 自增`++`
>
> `q=(++j)+(++j)+(++j);`：
>
> 括号   ===   自左向右   ===   `q`等于`j + j `再 `+ j`
>
> 第一次-加号   ===   自右向左   ===   `j + j`等于第二个j加上第一个j，即先自增2次，`j + 2 = 7`，结果`j + j = 7 + 7 = 14`
>
> 第二次-加号   ===   自右向左   ===   `q + j`等于`j + q`，即先自增1次，`j + 1 = 8`，结果`q + j = j + q = 8 + 14 = 22`

### 赋值运算符和赋值表达式

#### 赋值运算符

简单赋值运算符和表达式：简单**赋值运算符**为`=`。由`=`连接的式子称为**赋值表达式**。

其一般形式为：

```c
变量 = 表达式
```

> 赋值表达式的功能是计算表达式的值再赋予左边的变量。赋值运算符具有右结合性。因此：`a=b=c=5`，可以理解为`a=(b=(c=5))`

#### 复合的赋值运算符

在赋值符`=`之前加上其他二目运算符可以构成复合赋值符。如`+=`，`-=`，`*=`，`/]`，`%=`，`<<=`，`>>=`，`&=`，`^=`，`:=`

### 逗号运算符和逗号表达式

在C语言中逗号`.`也就是一种运算符，称为逗号运算符。其功能是把两个表达式连接起来组成一个表达式，称为逗号表达式。

一般表达式：

```c
表达式1，表达式2
```

其求值过程是分别求两个表达式的值，并以表达式2的值作为整个逗号表达式的值。

### 关系运算符和关系表达式

#### 关系运算符

在C语言中有以下关系运算符-

- `<`小于
- `<=`小于或等于
- `>`大于
- `>=`大于或等于
- `==`等于
- `!=`不等于

关系运算符都是双目运算符，其结合均为左结合。

#### 关系表达式

关系表达式的值时`真`和`假`，用`1`和`0`来表示。

### 逻辑运算符和逻辑表达式

#### 逻辑运算符

C语言提供了三种逻辑运算符：

- `&&`与运算
- `||`或运算
- `！`非运算

与运算符`&&`和或运算符`||`均为双目运算符，具有左结合性。<br>非运算符`!`为单目运算符，具有右结合性。

> 三者的优先级顺序：`!`(非) -> `&&`(与) -> `||`(或)

#### 逻辑表达式

一般形式：

```c
表达式 逻辑表达式 表达式
```

> 其中的表达式可以是表达式也可以是逻辑表达式，从而组成了嵌套的情形。

### 条件运算符和条件表达式

#### 条件运算符

条件运算符为`xx?xx:xx`，它是一个三目运算符，即有三个参与运算的量。

#### 条件表达式

其一般形式为：

```c
表达式1 ? 表达式2: 表达式3
```

其求值规则为：如果表达式1成立(为`True`)，则返回表达式2的值，否则返回表达式3的值。

### 🧭取地址运算符和取值运算符

在C语言中，想要获取某个变量的地址，可以使用取地址运算符`&`：

```c
&变量名
```

在C语言中，想要访问某个指针变量指向的数据，可以使用取值运算符`*`：

```c
*变量名
```

示例：

```c
#include <stdio.h>
int main() {
    char a='a';
    char f='f';
    char *A = &a;
    char *F = &f;
    printf("原本的样子(char-ascii):%c -> %d,%c -> %d\n",*A,*A,*F,*F);
    *A = *A - 32;
    *F = *F - 32;
    printf("原本的样子(char-ascii):%c -> %d,%c -> %d",*A,*A,*F,*F);
}
/////////////////运行结果////////////////
// 原本的样子(char-ascii):a->97,f->102 //
// 原本的样子(char-ascii):A->65,F->70  //
///////////////////////////////////////
```

### 🍟补充：运算符的优先级和结合性示意图

![示意图](https://gitee.com/acg-q/pic-go-images/raw/master//2021-02-23_15:41:13.png)

## ↕️格式化输入输出

#### 输出函数`printf`需要注意的点

使用`printf`函数时还需要注意一个问题，那就是输入输出表列中的求值顺序。不同的编译系统不一定相同，可以是从左到右，也可以从右到左。

```c
#include <stdio.h>
void main(){
    int i=8;
    printf("%d %d %d %d\n\n\n",++i,--i,i++,i--);
}
/////运行结果////
/// 8 8 7 8  //
///////////////
```

```
分析运行顺序：
1.先自增(++i)再自减(--i)
++i i=9 ==> i(a)
--i i=8 ==> i(b)
当前i=8
2.自右往左运算(p输出时的值)
i-- p=8 i=7
i++ p=7 i=8
i(b) p=8
i(a) p=8
3.调整输出顺序
 ++i --i  i++ i--
i(a) i(b) i++ i--
  8    8   7   8
```

> 结合猜想输出结果和真实输出结果，当前我的编译系统的输出函数`printf`就是自右向左运算的。

#### 输入函数`scanf`需要注意的点

- `scanf`函数中没有精度控制，如：`scanf("%5.2f",&a);`是非法的。不能企图用此语句出入小数点为两位的实数(浮点数)。

- `scanf`中要求给出变量地址，如给出变量名则出错。如：`scanf("%d",a);`是非法的，`scanf("%d",&a);`是合法的。

- 在输入多个数值数据时若格式控制串中没有非格式字符作为输入数据之间的间隔符则可以用空格，tab或者回车作为间隔。如果接收到的输入与要求的数据类型不同(即为非法数据)时该数据结束，例如，要求输入两个数值并赋值`a,b`(`scanf("%d%d",&a,&b);`)，但是在输入第一个数值时，输入`15a`，该输入环节直接结束，将`15`赋值给`a`，将`0`赋值给`b`。

- 在输入字符数据时，若格式控制符中无非格式字符，则认为所有输入的字符均为有效字符。

  例如：

  ```c
  #include <stdio.h>
  void main(){
      char a,b;
      printf("请输入a,b的大写：");
      scanf("%c%c",&a,&b);
      printf("a='%c',b='%c'\n",a,b);
      char c,d;
      printf("请输入c,d的大写：");
      scanf("%c %c",&c,&d);
      printf("c='%c',d='%c'",c,d);
  }
  /////////运行结果////////
  // 请输入a,b的大写：A B //
  // a='A',b=' '        //
  // 请输入c,d的大写：C D //
  // c='B',d='C'        //
  ////////////////////////
  ```

## 🔄程序语句

### ✅判断语句

#### `if`语句

第一种形式为基本形式：

```c
if(表达式) 语句
```

> 其语义是：如果表达式的值为真，则执行其后的语句，否则不执行该语句(仅一条语句)。
>
> ![if语句_基本样式_过程](https://gitee.com/acg-q/pic-go-images/raw/master//2021-02-24_13:28:23.png)

第二种形式为`if-else`：

```c
if（表达式）语句1;else 语句2;
```

![if语句_if-else_过程](https://gitee.com/acg-q/pic-go-images/raw/master//2021-02-24_13:32:22.png)

第三种形式为`if-else-if`：

```c
if(表达式1) 语句1;else if(表达式2) 语句2;else 语句3;
//////////////////////////////////////////////////
void main(){
    int c=1,d=2,a;
    scanf("%d",&a);
    if(c == a) printf("1");else if(d == a) printf("2");else printf("3");
}
```

![if语句_if-else-if_过程](https://gitee.com/acg-q/pic-go-images/raw/master//2021-02-24_13:37:53.png)

> 适用于多级分支判断

#### `switch`语句

C语言还提供了另一种用于多级分支的`switch`语句，其一般形式为：

````c
switch(表达式){
    case 常量表达式1: 语句1;
    case 常量表达式2: 语句2;
    case 常量表达式3: 语句3;
    case 常量表达式4: 语句4;
    default: 语句5;
}
````

其语义是：计算表达式的值，并逐个与其后的常量表达式值相比较，当表达式的值与某个常量表达式的值相等时，即执行其后的语句，然后不再进行判断，继续执行后面的`case`后的语句。如果表达式的值与所有case后的常量表达式均不相同时，则执行`default`后的语句。

> 如果在语句后面没有`break`,则会继续执行后面的语句，直到执行结束。

### 🔁循环语句

#### `goto`语句

`goto`语句是一种**无条件转移**语句，与`basic`中的`goto`语句相似。`goto`语句的使用格式为：

```c
goto 语句标号;
```

其中标号是一个有效的标识符，这个标识符加上一个`：`一起出现在函数内的某处，执行`goto`语句后，程序将跳转到该包好处并执行其后的语句。另外标号必须与`goto`语句同处于一个函数中，但可以不再一个循环层中。通常`goto`语句与`if`条件语句连用，当满足某个条件时，程序跳到标号处运行。

> 但是注意：`goto`语句通常不用，只要因为它将程序层次不清，但在多层嵌套退出时，用`goto`语句则比较合理。

#### `while`语句

`while`语句的一般形式为：

```c
while(表达式)语句
```

其中表达式时循环条件，语句为循环体。

`while`语句的语义时：计算表达式的值，当值为真(非0)时，执行循环体语句。

![while语句_过程](https://gitee.com/acg-q/pic-go-images/raw/master//2021-02-24_14:37:36.png)

#### `do-while`语句

`do-while`语句的一般形式为：

```c
do
	语句
while(表达式);
```

这个循环与`while`循环不同的在于：它先执行循环中的语句，然后再判断是否为真，如果为真则继续循环；如果为假，则中止循环。因此，`do-while`循环至少要执行一次循环语句。

![do-while语句_过程](https://gitee.com/acg-q/pic-go-images/raw/master//2021-02-24_15:15:14.png)

#### `for`语句

在C语言中，for语句使用最为灵活，它完全可以取代`while`语句。

它的一般形式：

```c
for(表达式1;表达式2;表达式3) 语句
```

`for`循环最容易理解的应用形式也是最容易理解的形式如下：

```c
for(循环变量赋初值;循环条件;循环变量增量) 语句
```

#### `break`和`continue`语句

##### `break`语句

`break`语句可以用来从循环体内跳出循环体，即提前结束循环，接着执行循环下面的语句。

`break`语句的一般形式：

```c
break;
```

##### `continue`语句

`continue`语句可以用来结束本次循环，即进入下一次循环。

`continue`语句的一般形式：

```c
continue;
```

## 🔢数组

### 数组的概念

数组：具有相同类型的数据组成的序列，是有序集合。<br>数组中的每一个数据称为**数据元素**，由其所在的位置序号(又称数组元素的下标)来区分。<br>用**数组名与下标**可以用统一的方式来处理数组中的所有元素，从而方便的实现处理一批具有相同性质数据的问题。

> 注意：数组元素有序不是指元素大小顺序

### 一维数组的定义和引用

#### 一维数组的定义

> 在C语言中使用数组必须先继续定义。

一维数组的定义方式为：

```c
类型说明符 数组名[常量表达式];
```

例如：`int a[10];`，它表示定义了一个整形数组，数组名为`a`，此数组有10个元素，10个元素都是整型变量！

> 注意：C语言不允许对数组的大小作动态定义，即数组的大小不依赖于程序运行过程中的变量值。例如：
>
> ```c
> void main(){
>     int n;
>     scanf("%d",&n);
>     int a[n];
> }
> ```

#### 一维数组的引用

数组元素是组成数组的基本单元，数组元素也是一种变量，其标识方法为数组名后跟一个下标。下标表示了元素在数组中的顺序号。

数组元素的一般形式：

```c
数组名[下标]
```

下标可以是整型常量或者整型表达式

#### 一维数组的初始化

给数组赋值的方法除了用赋值语句对数组元素逐个赋值外，还可采用初始化赋值和动态赋值的方法。

数组初始化赋值是指在数组定义时给数组元素赋予初值。数组初始化时在编译阶段进行的。这样将减少运行键，提高效率。

> 注意：之前用赋值语句或输入语句也可给数组素指定初值，时在运行时完成。

初始化赋值的一般形式为：

```c
类型说明符 数组名[常量表达式]={值，值，……值};
```

#### 🎯重点补充：一维数组在内存中的存放

![image-20210224170521656](https://gitee.com/acg-q/pic-go-images/raw/master//2021-02-24_17:05:27.png)

### 二维数组的定义和引用

#### 二维数组的定义

二维数组的定义的一般形式为：

```c
类型说明符 数组名[常量表达式][常量表达式];
```

例如：定义`a`为3x4(3行4列)的数组，`b`为5x10(5行10列)的数组。

```c
float a[3][4],b[5][10];
```

二维数组在概念上是二维的。

在C语言中，二维数组是按行排列

![二维数组_在内存中的排列方式示意图](https://gitee.com/acg-q/pic-go-images/raw/master//2021-02-24_18:24:21.png)

#### 二维数组的定义和初始化

二维数组的初始化方法：

```c
数据类型 数组名[常量表达式1][常量表达式2] = {初始化数据};
```

- 直接分行给二维数组赋初值。

  如：`int a[3][4]={{1,2,3,4},{5,6,7,8},{9,10,11,12}};`

- 可以将所有数据写在一个花括号内，按数组排列的顺序给个元素赋初值。

  如：`int a[3][4]={1,2,3,4,5,6,7,8,9,10,11,12};`

- 可以对部分元素赋初值。

  如：`int a[3][4]={{1},{5},{9}};`

  可以对各行中的某个元素赋初值。

  如：`int a[3][4]={{1}.{0,6},{0,0,11}};`

- 如果对全部元素都赋初值，则定义数组时对第一维的长度可以不指定，但第二维的长度不能省。

  如：`int a[3][4]={1,2,3,4,5,6,7,8,9,10,11,12};`

  它等价于：

  `int a[][4]={1,2,3,4,5,6,7,8,9,10,11,12};`

### 一维数组、二维数组的引用

```c
#include <stdio.h>
int main() {
    int b[3] = {0};
    printf("%d\n",b); // 6618612 地址
    printf("%d\n",b[0]); // 0
    printf("%d\n",*b); // 0
    int a[2][3]={0};
    printf("%d\n",a); // 6618624 地址
    printf("%d\n",a[0]); // 6618624 地址
    printf("%d\n",*a[0]); // 0
    printf("%d\n",a[0][0]); // 0
    printf("%d\n",**a); // 0
}
///运行结果////
// 6618612 //
// 0       //
// 0       //
// 6618624 //
// 6618624 //
// 0       //
// 0       //
// 0       //
/////////////
```

解析：

一维数组

```
b ==> b[3]的第一个元素的地址
*b ==> b[3]的第一个元素的地址的值
b[0] ==> b[3]的第一个元素
```

二维数组

```
a ==> a[2][3]的第一行第一列的元素的地址(第一个元素的地址)
a[0] ==> a[2][3]的第一行第一列的元素的地址(第一个元素的地址)
*a[0] ==> a[2][3]的第一行第一列的元素的地址(第一个元素的地址)的值
a[0][0] ==> a[2][3]的第一行第一列的元素
**a ==>
	==> a ==> a[2][3]的第一行第一列的元素的地址(第一个元素的地址)
	==> *a ==> a[2][3]的第一行第一列的元素的地址(第一个元素的地址)的值
		==> a[2][3]的第一行的数组的地址
	==> **a ==> a[2][3]的第一行第一列的元素的地址(第一个元素的地址)的值的值 
		==> a[2][3]的第一行的数组的地址的值
a+1 ==> a[2][3]的第二行第一列的元素的地址(第四个元素的地址)
```

> ## 结论：
>
> 得出一个结论，一维数组也好，二维数组也好，多维数组也罢，都完全复合这个**`*(a+i)=a[i]`**公式。
>
> > **`*(a+i)=a[i]`**
> >
> > **`*(*(a+i)+j)=a[i][j]`**
> >
> > **`*(*(*(a+i)+j)+k)=a[i][j][k]`**

### 🚀衍生：多维数组的定义

#### 定义三维数组

```c
float a[2][3][4];
```

多维数组元素在内存中的排列顺序：第一维的下标变化最慢，最右边的下标变化最快。

## 🧭指针

###  内存是如何存放变量的？

通过变量名对变量进行访问和存储是为了方便程序员而设计的，其实在内存中完全没有存储变量名的必要。

当编辑器想找要知道变量值的顺序如下：

- 已知变量名
- 从内存中获取该变量所存放的值`value`
- 再通过这个`value`在内存中寻找地址等于`value`项，并获取所其存放的值

### 指针和指针变量

通常我们所说的**指针，就是地址的意思**。C 语言中有专门的指针变量用于存放指针，跟普通变量不同，**指针变量存储的是一个地址**。<br>指针变量也有类型，它的类型就是存放的地址指向的数据类型。

![指针_变量名地址_地址](https://gitee.com/acg-q/pic-go-images/raw/master//2021-02-25_11:04:29.png)

### 指针变量

在C语言中指针变量的一般形式：

```c
类型名 *指针变量名;
```

### 🍟补充：避免访问未初始化的指针

由于未初始化的指针的所执行的地址是随机的，不清楚指针指向哪里，有可能会指向系统的关键代码

```c
#include <stdio.h>
int main() {
    int *a;
    *a = 123;
    return 0;
}
```

所以如上述一样直接访问指针变量是非常危险的。

更危险的是，偶尔这个指针变量里随机存放的是一个合法的地址，那么接下来的赋值就会导致那个位置的值莫名其妙地被修改。**这种类型的 Bug 是非常难以排查的**。

所以，在对指针进行间接访问时，必须确保它们已经被正确地初始化。

### 指针的运算

对指针的加减，只是对地址的位置进行改变(往前一个元素 or 往后一个元素)，并不是对指针地址存储的值进行改变。<br>整个内存可以看作一个数组，指针本身(`p`)对应于数组的下标，指针地址存储的值(`*p`)对应数组的数组元素，对指针的加减就是对下标的加减。

> 注意：指针绝不是数组，以上说辞只是类比，以便于理解。

### 指针和数组的区别

举个例子来区别指针和数组：遍历数组

✅通过指针实现遍历

```c
#include <stdio.h>
int main() {
    char str[] = "Hello World!";
    char *target = str;
    int count = 0;
    while(*target++ != '\0'){
        count++;
    }
#if(0)//便于理解，这两个等同
    while(*target != '\0'){
        count++;
        *target++;
    }
#endif
    printf("一共%d个。",count);
}
////运行结果////
// 一共12个。 //
//////////////
```

❎基于类似的代码进行实现

```c
#include <stdio.h>
int main() {
    char str[] = "Hello World!";
    int count = 0,i=0;
    while(*str++ != '\0'){
        count++;
    }
    printf("一共%d个。",count);
}
//////////////////编译结果/////////////////
// lvalue required as increment operand //
// 翻译：递增操作数需要左值                 //
//////////////////////////////////////////
```

> ### 什么是左值？
>
> C 语言的术语 lvalue 指用于识别或定位一个**存储位置的标识符**。（注意：**左值同时还必须是可改变的**）
>
> 引用自 [ ***什么是 lvalue，什么是 rvalue？***](https://fishc.com.cn/forum.php?mod=viewthread&tid=69833)

✅使用数组的下标进行实现

```c
#include <stdio.h>
int main() {
    char str[] = "Hello World!";
    int count = 0,i=0;
    while(str[i++] != '\0'){
        count++;
    }
    printf("一共%d个。",count);
}
////运行结果////
// 一共12个。 //
//////////////
```

**结论：数组名只是一个地址，而指针只是一个左值**

### 指针数组和数组指针

![指针数组_数组指针](https://gitee.com/acg-q/pic-go-images/raw/master//2021-02-25_14:26:57.png)

#### 指针数组

> 指针数组就是元素都是指针的数组。

```c
int *p[5];
```

| 下标 | 0       | 1       | 2       | 3       | 4       |
| ---- | ------- | ------- | ------- | ------- | ------- |
| 元素 | `int *` | `int *` | `int *` | `int *` | `int *` |

每一个元素都是整型指针。<br>指针数组是一个数组，每个数组元素存放一个指针变量。

> 指针数组的初始化等同于数组的初始化。

```c
#include <stdio.h>
int main() {
    int a=1,b=2,c=3,d=4,f=5;
    int *p[5] = {&a,&b,&c,&d,&f};
    for (int i = 0; i < 5; i++) {
        printf("p[%d]=%d\n", i, &p[i]);
    }
}
//////运行结果/////
// p[0]=6618592 //
// p[1]=6618600 //
// p[2]=6618608 //
// p[3]=6618616 //
// p[4]=6618624 //
//////////////////
```

#### 数组指针

> 数组指针就是指向数组的指针。

```c
#include <stdio.h>
int main() {
    int temp[5] = {1,2,3,4,5};
    int (*p)[5] = &temp;
    for(int i=0;i<5;i++){
        printf("%d\n",*(*p+i));
    }
}
//运行结果//
// 1    //
// 2    //
// 3    //
// 4    //
// 5    //
//////////
```

代码解析：

```
// *(*p) ==> *地址 ==> 地址(&temp)指向的值
// *p ==> p这个指针所指向的值 ==> &temp 地址 等于 数组temp的第一个元素的地址
// *p+i ==> p这个指针所指向的值+i ==> &temp+i 等于 数组temp的第(i+1)个元素的地址
// *(*p+i) ==> (p这个指针所指向的值+i)的值 ==> &temp+i 等于 数组temp的第(i+1)个元素的地址的值
```

### `void`指针

`void`指针赋值、引用

```c
#include <stdio.h>
int main() {
    int num = 5;
    int *a=&num;
    void *p;
    p=a;
    printf("a:%p",a);
    printf(" --- ");
    printf("p:%p\n",p);
```

`void`指针转换成`int`指针

```c
    printf("*a:%d",*a);
    printf(" --- ");
    // printf("p:%d\n",*p); // warning: dereferencing 'void *' pointer
    printf("p:%d\n",*(int *)p);
}
```

> 获取`void`指针对应的值时，需要先**强制类型转换**(`(int *)p`)，这样才能获取到指定地址的值。

> 注意：**不到万不得已，不要使用`void`指针。**在使用`void`指针时，**必须写注释**，不然后面无论是谁理解代码时，都会什么吃力。

### `NULL`指针

当你不清楚指针初始化时，该指向哪里时，这时候就可以初始化`NULL`；在对指针进行应用时，先检查指针是否为`NULL`。这种策略可以为你今后编写大型程序节省大量的调试时间。

```c
#define NULL ((void *)0)
```

`NULL`用于指针和对象，表示控制，指向一个不被使用的地址；而`\0`(`NUL`)表示字符串的结尾。

### 常量指针和指针常量

指向常量的指针，就是**常量指针**，<br>值是指针的常量，就是**指针常量**，<br>前者无法修改值，因为**指向的是常量**，<br>后者无法修改指向，因为**指针是常量**。

### 函数指针和指针函数

指向函数的指针，就是**函数指针**，<br>参数是指针的函数，就是**指针函数**。

#### 函数指针

函数指针`int (*p)();`

```c
int function();
int function(int num){
    return num * num;;
}
void main(){
    int (*p)(int);
    int num = 5;
    p = &function;
    printf("%d * %d = %d", num, num,(*p)(num));
}
```

#### 指针函数

指针函数`int *p();`

##### 以指针为参数的函数

```c
#include <stdio.h>
int f(int);
int fs(int (*p)(int), int num);
int f(int num) {
    return num * num;;
}
int fs(int (*p)(int), int num) {
    return (*p)(num);
}
void main() {
    int num = 5;
    int num2 = fs(f, num);
    printf("%d * %d = %d", num, num, num2);
}
```

##### 返回指针的函数

```c
#include <stdio.h>
int f(int);
int fs(int (*p)(int), int num);
int (*a(int))(int);
int f(int num) {
    return num * num;;
}
int fs(int (*p)(int), int num) {
    return (*p)(num);
}
int (*a(int op))(int num) {
    if (op) {
        return f;
    }
}
void main() {
    int num = 5;
    int (*p)(int);
    p = a('-');
    printf("%d * %d = %d", num, num, fs(p, num));
}
```

> 实现原理：函数调用，所有的指针都只是打的传参(址)，而不是反址。

## 💻函数

### 什么是函数

一个较大的程序可分为若干个**程序模块**，每个模块用来实现一个特定的功能，这样的模块被称为函数。<br>一个主函数可以有无数个子函数。

### 子函数

创建函数分三步：

- 声明有这么一个函数

  ```c
  #include <stdio.h>
  char *logo();
  ```

- 给函数写入内容

  ```c
  char *logo() {
      printf("logo");
      return "我是LOGO";
  }
  ```

- 调用函数

  ```c
  int main() {
      char *a = logo();
      printf("\n%s", a);
  }
  ```

### 形参和实参

函数中定义的参数就是形参，<br>调用函数时，传递的值就是实参。

### 传参和传址的区别

传参：函数中无论如何修改，都无法影响调用它的函数的值。<br>传址：函数中进行修改，调用它的函数的值也会发生改变。

**例子：传参**

```c
#include <stdio.h>
void dy();
void dy(int x) {
    x = 5;
    printf("dy x => %d\n",x);
}
int main() {
    int x=9;
    printf("main x => %d\n",x);
    dy(x);
    printf("main x => %d",x);
}
/////运行结果//////
// main x => 9 //
// dy x => 5   //
// main x => 9 //
/////////////////
```

**例子：传址**

```c
#include <stdio.h>
void dy();
void dy(int x) {
    x = 5;
    printf("dy x => %d\n",x);
}
int main() {
    int x=9;
    printf("main x => %d\n",x);
    dy(x);
    printf("main x => %d",x);
}
/////运行结果//////
// main x => 9 //
// dy x => 5   //
// main x => 5 //
/////////////////
```

> 传参 ==> 函数(局部)变量 <br>传址 ==> 全局变量

### 反参和反址

反参：返回参数值。<br>反址：由于参数是局部的，参数的地址也是局部的，所以反址失败。

## 🍩作用域

### 代码块作用域（`block scope`）

最常见的就是**代码块作用域**。所谓代码块，就是位于一对花括号之间的所有语句。

### 文件作用域（**file scope**）

任何在代码块之外声明的标识符都具有**文件作用域**，作用范围是从它们的声明位置开始，到文件的结尾处都是可以访问的。另外，函数名也具有文件作用域，因为函数名本身也是在代码块之外。

### 原型作用域（**prototype scope**）

**原型作用域**只适用于那些在函数原型中声明的参数名。我们知道函数在声明的时候可以不写参数的名字（但参数类型是必须要写上的）。

### 函数作用域（**function scope**）

**函数作用域**只适用于 goto 语句的标签，作用将 goto 语句的标签限制在同一个函数内部，以及防止出现重名标签。

## 🍔生存期

### 静态存储期(`static storage duration`)

具有文件作用域的变量属于**静态存储期**，函数也属于**静态存储期**。属于**静态存储期**的变量在程序指向期间将一直占据存储空间，直到程序关闭才能释放。

### 自动存储期(`automatic storage duration`)

具有代码块作用域的变量一般情况下属于**自动存储期**。属于**自动存储期**的变量在代码块结束时将自动释放存储空间。

## 💿存储类型

C语言中提供了5中不同的存储类型：

- `auto`
- `register`
- `static`
- `extern`
- `typedef`

### 自动变量(`auto`)

在代码块中声明的变量默认的存储类型就是自动变量，使用关键字 `auto` 来描述。

由于这是默认的存储类型，所以不写`auto`是完全没有问题的。

### 寄存器变量(`register`)

将一个变量声明为寄存器变量，那么该变量就是可能被存放于CPU的寄存器中。

寄存器变量和自动变量在很多方面的是一样的，他们都拥有代码块作用域，自动存储期和空连接属性。

不过，当把变量声明为寄存器变量后，那么你就没有办法通过取址运算符来获取该变量的地址。

### 静态局部变量(`static`)

使用`static`来声明局部变量，那么就可以将局部变量指定为静态局部变量。

`static`使得局部变量具有静态存储期限，所以它的生存期与全部变量一样，直到程序结束才释放。

### 外部变量(`extern`)

 `extern` 关键字是用于告诉编译器这个变量或函数在其他的地方已经定义过了.

### 重命名变量(`typedef`)

`typedef`关键字是用于告诉编译器这个变量或函数已经重命名了。

## 🙃递归

### 递归的含义

递归从原理上来说就是函数**调用自身**这么一个行为。

### 编写递归程序需要注意的地方

递归程序需要正确设置结束条件，否则递归程序会一直走下去，直到崩溃。

## 🏢结构体

C语言结构体（Struct）从本质上讲是一种自定义的数据类型，只不过这种数据类型比较复杂，是由 int、char、float 等基本类型组成的。你可以认为结构体是一种聚合类型。

### 结构体声明

```c
struct 结构体名称{
    类型名 结构体成员1;
    类型名 结构体成员2;
};
```

### 访问结构体

为了访问结构体成员，需要引入新的运算符`.`，例如：`Students.name`。

```c
#include <stdio.h>

struct Students {
    char *name;
    int age;
};
void main() {
    struct Students students;
    students.name = "六记";
    students.age = 5;
    printf("%s",students.name);
}
```

```c
#include <stdio.h>
struct Students {
    char *name;
    int age;
} students;
void main() {
    students.name = "六记";
    students.age = 5;
    printf("%s",students.name);
}
```

### 结构体初始化

```c
#include <stdio.h>
struct Students {
    char *name;
    int age;
};
void main() {
    struct Students students={
            "六记",//顺序赋值
            .age=5//指定赋值
    };
    printf("姓名：%s  年龄：%d\n",students.name,students.age);
}
```



## 🍟补充

### include中双引号和尖括号的区别

尖括号：表示只在系统默认目录或者括号内的路径查找，通常用于包含系统中自带的头文件。（指在linux下编程）<br>双引号：引用非标准库的头文件，编译器从用户的工作目录开始搜索，如果未找到则去系统默认目录查找，通常用于包含程序作者编写的头文件。

### `strcmp()`函数：比较两个字符串

```c++
char str1[] = "123";
char str2[] = "123";
ret = strcmp(str1,str2);
```

- 如果返回值(`ret`)**小于** 0，则表示 str1 小于 str2。
- 如果返回值(`ret`)**大于** 0，则表示 str1 大于 str2。
- 如果返回值(`ret`)**等于** 0，则表示 str1 等于 str2。

### `strcpy`、`strncpy`、`strtoul`

- `strcpy(a,b);`：把 **b** 所指向的字符串复制到 **a**，返回值为指针

- `strncpy(a,b,n);`：把 **b** 所指向的字符串复制到 **a**，最多复制 **n** 个字符，返回值为指针

  - 例子：

    ```c++
    char a[8];
    char b[] = "12345678";// 12345678\0 ==> 9个字节，\0是一个字节
    strcpy(a,b);// 超出a的界限
    strncpy(a,b,sizeof(a)-1);//这样才能保住赋值不会超出限制
    ```

- `strtoul()`



### 什么是`uint8_t`、`uint16_t`？为什么使用它？

>  方便代码的维护，依旧后期维护
>
> 在C99标准中定义了这些数据类型，具体定义在：<stdint.h>中

```c
typedef   signed          char int8_t;
typedef   signed short     int int16_t;
typedef   signed           int int32_t;
typedef   signed       __INT64 int64_t;
 
/* exact-width unsigned integer types */
typedef unsigned          char uint8_t;
typedef unsigned short     int uint16_t;
typedef unsigned           int uint32_t;
typedef unsigned       __INT64 uint64_t;
 
/* 7.18.1.2 */
/* smallest type of at least n bits */
/* minimum-width signed integer types */
typedef   signed          char int_least8_t;
typedef   signed short     int int_least16_t;
typedef   signed           int int_least32_t;
typedef   signed       __INT64 int_least64_t;
 
/* minimum-width unsigned integer types */
typedef unsigned          char uint_least8_t;
typedef unsigned short     int uint_least16_t;
typedef unsigned           int uint_least32_t;
typedef unsigned       __INT64 uint_least64_t;
 
/* 7.18.1.3 */
/* fastest minimum-width signed integer types */
typedef   signed           int int_fast8_t;
typedef   signed           int int_fast16_t;
typedef   signed           int int_fast32_t;
typedef   signed       __INT64 int_fast64_t;
 
/* fastest minimum-width unsigned integer types */
typedef unsigned           int uint_fast8_t;
typedef unsigned           int uint_fast16_t;
typedef unsigned           int uint_fast32_t;
typedef unsigned       __INT64 uint_fast64_t;
 
/* 7.18.1.4 integer types capable of holding object pointers */
#if __sizeof_ptr == 8
typedef   signed       __INT64 intptr_t;
typedef unsigned       __INT64 uintptr_t;
#else
typedef   signed           int intptr_t;
typedef unsigned           int uintptr_t;
#endif
 
/* 7.18.1.5 greatest-width integer types */
typedef   signed     __LONGLONG intmax_t;
typedef unsigned     __LONGLONG uintmax_t;
```

### 输出字符

| 控制符                    | 说明                                                         |
| ------------------------- | ------------------------------------------------------------ |
| %d                        | 按十进制整型数据的实际长度输出。                             |
| %ld                       | 输出长整型数据。                                             |
| %md                       | m 为指定的输出字段的宽度。如果数据的位数小于 m，则左端补以空格，若大于 m，则按实际位数输出。 |
| %u                        | 输出无符号整型（unsigned）。输出无符号整型时也可以用 %d，这时是将无符号转换成有符号数，然后输出。但编程的时候最好不要这么写，因为这样要进行一次转换，使 CPU 多做一次无用功。 |
| %c                        | 用来输出一个字符。                                           |
| %f                        | 用来输出实数，包括单精度和双精度，以小数形式输出。不指定字段宽度，由系统自动指定，整数部分全部输出，小数部分输出 6 位，超过 6 位的四舍五入。 |
| %.mf                      | 输出实数时小数点后保留 m 位，注意 m 前面有个点。             |
| %o                        | 以八进制整数形式输出，这个就用得很少了，了解一下就行了。     |
| %s                        | 用来输出字符串。用 %s 输出字符串同前面直接输出字符串是一样的。但是此时要先定义字符数组或字符指针存储或指向字符串，这个稍后再讲。 |
| %x（或 %X 或 %#x 或 %#X） | 以十六进制形式输出整数，这个很重要。                         |

## 🍛主要参考资料

- [小甲鱼出品-《带你学C带你飞(第一季)》](https://fishc.com.cn/forum.php?mod=forumdisplay&fid=329)
- 