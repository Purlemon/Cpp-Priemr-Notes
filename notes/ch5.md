# 第五章 语句

## 简单语句

- **表达式语句**：一个表达式末尾加上分号，就变成了表达式语句
- **空语句**：只有一个单独的分号
- **复合语句（块）**：用花括号 `{}`包裹起来的语句和声明的序列。一个块就是一个作用域

## 条件语句
### if语句
- **悬垂else**（dangling else）：用来描述在嵌套的`if else`语句中，如果`if`比`else`多时如何处理的问题。C++使用的方法是`else`匹配最近没有配对的`if`
### switch语句
- `case`标签必须是**整型常量表达式**
- `case`匹配成功，顺序执行之后的所有语句，直到`break`或`switch`结尾  
```cpp
switch (ch) { 
	case'a':
		++ach;
	case'e':
		++ech;
	case'i':
		++ich;
	case'o':
		++och;
}//若ch=e，则ech，ich，och均递增
```
- 如果没有任何一个`case`匹配，将执行`default`标签后的语句  
  - 即使不准备在`default`下做任何工作，也应该定义一个`default`方便阅读
  
## 迭代语句

### while语句
- 条件部分是一个表达式或一个**带初始化的**变量声明，*如：`while(int i)//错误：必须包含初始化`*
- 定义在条件部分或循环体内的变量每次迭代都经历从创建到销毁的过程
- **`do while`语句**：先执行循环体，再检查条件

### for语句
- `for`语句可以省略掉 `init-statement`， `condition`和 `expression`的任何一个；**甚至全部**
- `init-statement`可以定义多个对象，但只能有**一条**声明语句
```cpp  
for(int i, j;;)                   //正确
for(int i = 0, j = 0;;)           //正确
for(int i = 0, int j = 0;;)       //错误
```
### 范围for语句
`for (declaration: expression) statement`
- `expression`是带有能返回迭代器的`begin` `end`成员的容器
```cpp
//等价于如下传统for
for (auto beg = v.begin(), end = v.end(); beg != v.end(); ++beg) 
{//由于预存了end()，添加/删除元素可能使其失效     
  auto r = *beg;
}
```
## 跳转语句

- **break**：`break`语句负责终止离它最近的`while`、`do while`、`for`或者`switch`语句，并从这些语句之后的第一条语句开始继续执行
- **continue**：终止最近的循环中的当前迭代并立即开始下一次迭代。只能在`while`、`do while`、`for`循环的内部
- **goto**：`goto lable; lable: return`无条件跳转到同一函数内的带标签语句
  - 标签标示符可以和其他实体标示符同名
  - `goto`语句和转向的语句位于同一函数内
```cpp
  if(error0_occur){
      goto err_exit;
  }
  return h;
err_exit:
  CloseHandle(h);
  return nullptr;
```
