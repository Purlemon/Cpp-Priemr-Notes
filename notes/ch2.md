# 第二章 变量和基本类型

## 基本内置类型  
        
### 算术类型
| 类型 | 含义 | 最小尺寸|
|---|---|---|
| `bool` | 布尔类型  | 8bits |
| `char`| 字符 | 8bits |
| `wchar_t` | 宽字符 | 16bits |
| `char16_t` | Unicode字符 | 16bits |
| `char32_t` | Unicode字符 | 32bits |
| `short` | 短整型 | 16bits |
| `int` | 整型 | 16bits  |
| `long` | 长整型 | 32bits |
| `long long` | 长整型 | 64bits  |
| `float` | 单精度浮点数 | 6位有效数字 |
| `double` | 双精度浮点数 | 10位有效数字 |
| `long double` | 扩展精度浮点数 | 10位有效数字 |
- 可寻址的最小内存块称为“字节（byte）”，储存的基本单元称为“字（word）”  
  - 1 byte=8 bit  
  - 1 word= 32 bit

### 带符号类型和无符号类型  
- `int`、`short`、`long`、`long long`都是带符号的，在这些类型名称前添加`unsigned`就可以得到无符号类型
- **`unsigned int`可以缩写成`unsigned`**  
- `char`会表现为`signed char`或`unsigned char`，由编译器决定

### 如何选择类型
- 1.当明确知晓数值不可能是负数时，选用无符号类型
- 2.使用`int`执行整数运算。一般`long`的大小和`int`一样，而`short`常常显得太小。除非超过了`int`的范围，选择`long long`
- 3.算术表达式中不要使用`char`或`bool`。如果使用`char`应明确指定它的类型是`sigened char`或者`unsigned char`  
- 4.浮点运算选用`double`  

### 类型转换
- 非布尔型赋给布尔型，初始值为0则结果为false，否则为true。  
```cpp
int i=42;
if(i)           //if的值将为true  
  i=0；
```
- 布尔型赋给非布尔型，初始值为false结果为0，初始值为true结果为1。
- 超出范围的值赋给无符号类型，结果是初始值对无符号类型表示数值总数取模后的余数  
  （如果是负数，[会直接使用负数的补码表示结果](https://blog.csdn.net/Songbai_Pu/article/details/9172689)，*如：将-1赋给8 bit的`unsigned char`结果是255*）  
 - 超出范围的值赋给带符号数，结果是**未定义的（undefined）**  
 - **当算术表达式中既含有`int`又含有无符号数时,`int`值将会转换为无符号数**  
 ```cpp
 int i=1;
 unsigned j=-1;
 cout << i*j ;          //输出4294967295
 ```  
 
 ### 字面值常量
 字面值常量（literal constant），“字面值”是指只能用它的值称呼它，“常量”是指其值不能修改。每个字面值都有相应的类型，3.14是`double`型，2是`int`型。只有内置类型存在字面值  
 - **1.整型字面值**  
 用十进制（*如：24*）、八进制（以0开头，*如：024*）、十六进制（以0x开头，*如：0x24*）表示  
   - 十进制字面值是带符号数，在能容纳的情况下取`int`、`long`、`long long`中最小  
     - 形如-42的十进制字面值，那个负号并不在字面值之内，它的作用仅仅对字面值取负而已
   - 八进制和十六进制字面值是带符号数或无符号数，在能容纳的情况下取`int`、`unsigned int`、`long`、`unsigned long`、`long long`、`unsigned long long`中最小  
   - 在整型后加**后缀**可指定类型 
     - u或U：`unsigned int`、`unsigned long`、`unsigned long long`中最小  
     - l或L：`long`、`unsigned long`、`long long`、`unsigned long long`中最小  
     - ll或LL：`long long`、`unsigned long long`中最小  
     - U可以和L混用，如UL或LU：`unsigned long`、`unsigned long long`中最小  
- **2.浮点数字面值**  
用十进制或科学计数法（指数用E或e）表示，默认为`double`，*如：3.14、3.14e1*
  - 在浮点数后加**后缀**可指定类型  
    - f或F：`float`
    - l或L；`long double`  
- **3.字符和字符串字面值**  
  - 由单引号括起来的一个字符称为char型字面值，*如：'a'*
  - 由双引号括起来的零个或多个字符称为字符串字面值，*如："Hello"*
    - 字符串字面值实际长度比内容多1，编译器自动在结尾处添加空字符（'\0'）
  - 在字符前加**前缀**可指定类型，*如：L‘a’、u8"hi!"*  
    - u：char16_t  
    - U：char32_t  
    - L：wchar_t  
    - u8：char（UTF-8,用8 bit编写一个Unicode字符，仅用于字符串字面常量）
- **4.布尔字面值**  
  true和false  
- **5.转义序列**  
  - 非打印字符和特殊字符（如单引号、双引号、反斜杠）都要写为转义字符（以反斜杠开头），下列转义序列被当作一个字符使用  
  - 也可以使用泛化的转义序列
    - \后加3个以内八进制数，若超过3个，只有前3个数字与\构成转义序列，*如：\12*  
    - \x后加多个十六进制数，*如：\x1234*
    
 | 字符| 转义序列 | 字符| 转义序列 |字符| 转义序列 |
 | --- | ---  | --- | ---  |--- | ---  |
 | 换行符 | \n | 纵向制表符 | \v |  横向制表符 | \t  | 回车符 | \r | 
 | 反斜线 | \\\  | 退格符 | \b |  问号 | \\? |  进纸符 | \f |  响铃符 | \a | 
 | 单引号 | \\'  | 双引号 | \\" |  

## 变量  
**变量**提供一个**具名**的、可供程序操作的存储空间。   `C++`中**变量**和**对象**一般可以互换使用。

### 变量定义  
- **定义形式**：类型说明符（type specifier） + 一个或多个变量名组成的列表  
*如`int sum = 0, value, units_sold = 0;`*  
- 


 
 
 
 
 
 
