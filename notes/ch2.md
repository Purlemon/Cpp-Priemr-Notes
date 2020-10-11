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

