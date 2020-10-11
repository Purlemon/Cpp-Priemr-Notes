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
- 1 byte=8 bit  1 word= 32 bit

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
  （如果是负数，[会直接使用负数的补码表示结果](https://blog.csdn.net/Songbai_Pu/article/details/9172689)，如：将-1赋给8 bit的`unsigned char`结果是255）  
 - 超出范围的值赋给带符号数，结果是**未定义的（undefined）**  
 - **当算术表达式中既含有`int`又含有无符号数时,`int`值将会转换为无符号数**  
 ```cpp
 int i=1;
 unsigned j=-1;
 cout << i*j ;          //输出4294967295
 ```  
 
 ### 字面值常量
 字面值常量（literal constant），“字面值”是指只能用它的值称呼它，“常量”是指其值不能修改。每个字面值都有相应的类型，3.14是`double`型，2是`int`型。只有内置类型存在字面值  
 - 1.整型字面值  
 整形字面值常量可以用十进制、八进制（以0开头）、十六进制（以0x开头）表示  
  ```
  20    //十进制           024//八进制                0x14//十六进制                      
  ```  
    - 十进制字面值是带符号数，在能容纳的情况下取`int`、`long`、`long long`中最小
    - 八进制和十六进制字面值是带符号数或无符号数，在能容纳的情况下取`int`、`unsigned int`、`long`、`unsigned long`、`long long`、`unsigned long long`中最小  

 
 
 
 
 
 
