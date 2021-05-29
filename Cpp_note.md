## OJ框架：

```c++
#include <bits/stdc++.h>

#pragma GCC optimize("O3")
#pragma GCC diagnostic error "-std=c++11"
//#pragma comment(linker, "/STACK:102400000,102400000")
#define REP(i, a, b) for(int i = a; i < b; ++i)
#define debug(x) { cerr << #x << '=' << x << "\n"; }
#define Arr(a, l, r) { cerr << #a << " = {"; REP(_, l, r) cerr << ' ' << a[_]; cerr << " }\n"; }
#define mset(a,b) memset(a,b,sizeof(a))
#define mkpr make_pair
#define ll long long
#define print(x) cout<<x<<"\n"

using namespace std;

int main(){
  ios::sync_with_stdio(false);cin.tie(NULL);cout.tie(NULL);

  ...your code

  return 0;
}
```

---

#### cout保留小数点后两位

```c++
cout<<setiosflags(ios::fixed)<<setprecision(2);
```

###### 保留有效数字去掉setiosflags(ios::fixed)即可

---

### C++内存

![cppmem](.//imgs/cppmemory.png)

虚拟内存技术使得每个进程都可以独占整个内存空间，地址从零开始，直到内存上限。 每个进程都将这部分空间（从低地址到高地址）分为六个部分：

* TEXT段：整个程序的代码，程序加载运行时，该段内存为只读区域，并且为共享的，当有多个相同进程(Process)存在时，共用同一个text段。`ROdata`段（详见DATA段）和TEXT段通常合并到一个Segment（Text Segment）中，操作系统将这个Segment的页面只读保护起来，防止意外的改写。
* DATA又称GVAR（global value）：用来存放程序中已经初始化的非零全局变量。其中data有分为可读写区域和只读区域：
  - 读写区域(RW)：存放非零全局变量、静态变量
  - 只读区域(RO)：存放常量
* BSS（Block Started by Symbol）段：**初始化为0或未初始化**的全局变量和静态变量。
* HEAP（堆空间）：动态内存区域，使用`malloc`，`make_shared`或`new`申请的内存。
* 未使用的内存。
* STACK（栈空间）：局部变量、参数、返回值都存在这里，函数调用开始会参数入栈、局部变量入栈；调用结束依次出栈。

其中堆空间和栈空间的大小是可变的，堆空间从下往上生长，栈空间从上往下生长。

由于常量存储在TEXT段中，所有对常量的赋值都将产生`segment fault`异常。

可以认为BSS段中的所有字节都是0。因为未初始化的全局变量、静态变量都在BSS段中， 所以它们都会被初始化为0，同时类的成员变量也会被初始化为0，但编译器不保证局部变量的初始化。

> 在C++中，如果类中有虚函数，那么它就会有一个虚函数表的指针__vfptr，在类对象最开始的内存数据中。之后是类中的成员变量的内存数据。注意要考虑对齐。

[Content origin1](https://harttle.land/2015/07/22/memory-segment.html)|||[Content origin2](https://vites.app/article/dev/8a9fa889.html)|||[Content origin3](https://www.zhihu.com/question/26224882)

[待看](http://chenqx.github.io/2014/09/25/Cpp-Memory-Management/)

---

### `const`&`point`

```c++
// 指针常量
int * const p = &a;
// 常量指针
const int* p = &a;
int const * p = &a;
```

- 如果const位于*的右侧，则const就是修饰指针本身，即指针本身是常量（指针常量）
- 如果const位于*的左侧，则const就是修饰指针所指向的变量，即指针指向常量（常量指针）

引用是一种指针常量

---

## Lambda函数

```c++
[capture list](parameter list)[mutable]->return type {function body}
```

* `capture list`为**捕获列表**，变量或引用在捕获后才能被`lambda`使用，编译器会为`lambda`创建一个类和类对象，**捕获参数**成为对象**数据成员**。
  * `[]` 不捕获任何变量
  * `[&]` 以**引用**方式捕获外部作用域的所有变量
  * `[=]` 以**赋值**方式捕获外部作用域的所有变量
  * `[=, &foo]` 以赋值方式捕获外部作用域所有变量，以引用方式捕获foo变量
  * `[bar]` 以赋值方式捕获bar变量，不捕获其它变量
  * `[this]` 捕获当前类的this指针，让lambda表达式拥有和当前类成员同样的访问权限，可以**修改类的成员变量，使用类的成员函数**。如果已经使用了&或者=，就默认添加此选项。
* 如果需要修改捕获的变量，则可以加上`mutable`关键字
* 编译器无法推断`function body`返回值时，需要加上`return type`

## 智能指针

### `shared_ptr`

* 不能将一个**内置指针**隐式转为一个**智能指针**

  ```c++
  shared_ptr<int> p1 = new int(1024); // 错误
  shared_ptr<int> p2(new int(1024));  // 正确
  ```

* 一个用来初始化**智能指针**的**普通指针**必须指向**动态内存**

* 推荐使用`make_shared`而不是`new`创建

* 引用计数为0会自动释放其指向的内存

* 动态绑定**删除器**：

  ```c++
  shared_ptr<cls> p(&obj, delete_func);	// 运行时绑定
  unique_ptr<cls, decltype(delete_func)*> p(&obj, delete_func); // 编译时绑定，删除器是指针的一部分
  ```

  

### `unique_ptr`

* 不能拷贝或赋值`unique_ptr`，但可：

  ```c++
  unique_ptr<string> p2(p1.release());
  p2.reset(p1.release());
  p2.reset(std::move(p1));
  ```

### `weak_ptr`

* 防止循环引用，不占用所有权

* 不能直接访问，需要：

  ```c++
  if(shared_ptr<int> np = wp.lock()){
      // 操作np
  }
  ```

  

---

## 虚函数

* 在子类**覆盖虚函数**时加上`override`关键字使得**编译器**能够发现是否**正确覆盖**
* 可以使用`base->Cls::vfunc()`回避虚函数机制
* 在**虚函数**声明语句**分号之前**加上**`=0`**可以将该虚函数声明为**纯虚函数**（Pure virtual function）；该做法只能在类内部
* 含有**纯虚函数**的类时抽象基类，不能够创建抽象基类的对象

#### 实现机制——虚表

每个包含虚函数类的对象都拥有一个虚表，编译器会在类中添加一个指针`__vptr`，对象创建则该指针会指向虚表。所以对象在在向上转型时，**虚表指针`__vptr`**亦是**基类成员**部分，所以**基类指针**可以访问到**派生类的虚表指针**，实现了**动态绑定**。

动态绑定要符合以下条件：

* 通过指针调用**虚函数**
* upcast

---

## 派生类向基类转换可访问性？

待写

---

## 继承

* `public`继承：正常继承，一切常态

* `protected`继承：基类**公共成员**成为派生类**保护成员**

* `private`继承：基类**公共成员**及**保护成员**成为派生类**私有成员**

* 使用`using`可以改变个别成员的可访问性

  ```c++
  class B:private A{
      public:
      	using A::var;
  }
  ```

  



* 友员关系不能继承，每个类自己控制各自成员访问权限

## 右值引用

* 通过`&&`而非`&`获得**右值引用**
* 只能绑定到一个**将要销毁**的对象
* 不能将**右值引用**直接绑定到**左值**上，但可以通过`std::move`将**左值**转化为**右值引用类型**

