# 第七章 类

## 定义抽象数据类型

### `this`
- 类成员函数通过隐式参数`this`来访问调用它的对象
- `this`是*指向非常量的常量指针*，不允许改变其中的地址
```cpp
string isbn() {return bookNo;}
string isbn() {return this->bookNo;}   //等价
```
### `const`常量成员函数
```cpp
string isbn() const {return bookNo;}
```
- `const`表示`this`是指向常量的指针
- 常量成员函数不能改变调用它的对象的内容

### 在类外部定义成员函数
- 使用作用域运算符`::`
- 返回类型、参数列表、函数名都要和类中声明保持一致
```cpp
int Student::GetName() {return name;}   //GetName为Student类中的函数定义
```
### 返回`this`对象的函数
```cpp
Student& Add(Student& S1)
{//将两个Student的age相加，之后返回调用这个函数的对象
age += S1.age;
return *this;
}
```
### 类的构造函数
- 不能被声明为`const`
- 没有返回值
- 只有在没有任何构造函数时才存在默认构造函数；如果定义了一些其他的构造函数，除非再定义默认构造函数，否则类将没有默认构造函数
```cpp
Student() = default;     //默认构造函数
Student(int a, string s): age(a), name(s) { }   //构造函数初始值列表
```
## 访问控制与封装

- **访问说明符**：一个类可包含0个或多个
  - `public`：定义在 `public`后面的成员在整个程序内可以被访问。
  - `private`：定义在 `private`后面的成员只能被类的成员函数访问，但不能被使用该类的代码访问。
- 使用 `class`或者 `struct`：
  - `class`：在第一个访问说明符之前的成员是 `priavte`的。
  -  `struct`：在第一个访问说明符之前的成员是 `public`的。

### 友元
- 允许特定的**非成员函数**访问一个类的**私有成员**。
- 友元的声明以关键字 `friend`开始。 `friend Sales_data add(const Sales_data&, const Sales_data&);`表示非成员函数`add`可以访问类的非公有成员。
- 友元声明**仅仅指定权限，并不是真正的声明**。还需要专门的另外声明。
- 通常将友元声明成组地放在**类定义的开始或者结尾**。
- 友元类不具有传递性，每个类只对自己的友元负责。
- 把类成员函数声明为友元，需要指出该成员函数属于哪个类`::`

## 类的其他特性

- 成员函数作为内联函数 `inline`：
  - **定义**在类内部的函数是**自动内联**的。
  - 在类外部定义的成员函数，也可以在声明时显式地加上 `inline`。
- **可变数据成员**`mutable` ：
  - `mutable int access_ctr;`
  - 永远不会是`const`，即使它是`const`对象的成员。
- 类内初始值
  - 必须用`=`或`{}`
- 类成员类型不能是自己，但可以是自身的引用或指针
