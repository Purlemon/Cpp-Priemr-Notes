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
	Student& Add(Student& S1) {
	age += S1.age;
	return *this;
  }//将两个Student的age相加，之后返回调用这个函数的对象
```
