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

## 类的作用域
- 一个类就是一个作用域。
- 函数的**返回类型**通常在函数名前面，因此当成员函数定义在类的外部时，返回类型中使用的名字都位于类的作用域之外。
- 如果成员使用了外层作用域中的某个名字，而该名字代表一种**类型**，则类不能在之后重新定义该名字。
- 类中的**类型名定义**都要放在一开始。

## 构造函数再探
- `const`或者引用类型的数据，只能用列表初始化，不能在构造函数体中赋值。
- 成员初始化顺序与在类定义中出现的顺序一致

### 委托构造函数
```cpp
class Sales_data {
public:
	//非委托构造函数
	Sales_data(string s, int cut, double price) :
		bookNo(s), sold(cnt), revebue(cnt* price) {}
	//其余构造函数全部委托给另一个构造函数
	Sales_data() :Sales_data("", 0, 0) {}
	Sales_data(string s) :Sales_data(s, 0, 0) {}
	Sales_data(string s, double price) :Sales_data(s, 0, price) {}
};
```
### 隐式的类型转换
- 如果构造函数**只接受一个实参**，则它实际上定义了转换为此类类型的**隐式转换机制**。这种构造函数又叫**转换构造函数**
- 编译器只会自动地执行`仅一步`隐式类型转换。
- 抑制构造函数定义的隐式转换：
  - 将构造函数声明为`explicit`加以阻止，只对一个实参的构造函数有效。
  - 只能在类内声明时使用`explicit`，在类外部定义时不应重复。
  - `explicit`构造函数只能用于直接初始化，不能用于拷贝形式的初始化。
  - 可用`static_cast`强制转换使用了`explicit`的构造函数
 ```cpp
class Sales_data {
public:
	Sales_data(): bookNo(""), sold(0) {}
	explicit Sales_data(string s) : bookNo(s), sold(0){}
	explicit Sales_data(double price) : bookNo(""), sold(price){}
	Sales_data(string s, double price) :Sales_data(s, price) {}
};
```
### 聚合类 （aggregate class）

- 满足以下所有条件：
  - 所有成员都是`public`的。
  - 没有定义任何构造函数。
  - 没有类内初始值。
  - 没有基类，也没有`virtual`函数。
- 可以使用一个花括号括起来的成员初始值列表，初始值的顺序必须和声明的顺序一致。
```cpp
struct Data{
    int ival;
    string s;
};
Data vall = {0, "Anna"};
```

### 字面值常量类

- `constexpr`函数的参数和返回值必须是字面值。
- **字面值类型**：除了算术类型、引用和指针外，某些类也是字面值类型。
- 数据成员都是字面值类型的聚合类是字面值常量类。
- 如果不是聚合类，则必须满足下面所有条件：
  - 数据成员都必须是字面值类型。
  - 类必须至少含有一个`constexpr`构造函数。
  - 如果一个数据成员含有类内部初始值，则内置类型成员的初始值必须是一条常量表达式；或者如果成员属于某种类类型，则初始值必须使用成员自己的`constexpr`构造函数。
   - `constexpr`构造函数可以声明为`=default`，且函数体为空。
  - 类必须使用析构函数的默认定义，该成员负责销毁类的对象。
## 类的静态成员

- 非`static`数据成员存在于类类型的每个对象中，`static`数据成员独立于该类的任意对象而存在。
- 每个`static`数据成员是与类关联的对象，并不与该类的对象相关联。
- 声明：
  - 声明之前加上关键词`static`。
- 使用：
  - 使用**作用域运算符**`::`直接访问静态成员:`Account::rate();`
  - 也可以使用对象访问：`ac.rate();` `ac->rate();`
- 定义：
  - 在类外部定义时不用加`static`。
- 初始化：
  - 通常不在类的内部初始化，而是在定义时在外部进行初始化，如 `double Account::interestRate = initRate();`
  - 如果一定要在类内部定义，则要求必须是字面值常量类型的`constexpr`，`static constexpr int period = 30`
