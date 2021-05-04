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

#### cout保留小数点后两位

```c++
cout<<setiosflags(ios::fixed)<<setprecision(2);
```

###### 保留有效数字去掉setiosflags(ios::fixed)即可

### C++内存

![cppmem](/Users/rabbyt/workspace2019/Mynote/imgs/cppmemory.png)

虚拟内存技术使得每个进程都可以独占整个内存空间，地址从零开始，直到内存上限。 每个进程都将这部分空间（从低地址到高地址）分为六个部分：

* TEXT段：整个程序的代码，程序加载运行时，该段内存为只读区域，并且为共享的，当有多个相同进程(Process)存在时，共用同一个text段。`ROdata`段（详见DATA段）和TEXT段通常合并到一个Segment（Text Segment）中，操作系统将这个Segment的页面只读保护起来，防止意外的改写。
* DATA又称GVAR（global value）：用来存放程序中已经初始化的非零全局变量。其中data有分为可读写区域和只读区域：
  - 读写区域(RW)：存放非零全局变量、静态变量
  - 只读区域(RO)：存放常量
* BSS（Block Started by Symbol）段：**初始化为0或未初始化**的全局变量和静态变量。
* HEAP（堆空间）：动态内存区域，使用`malloc`或`new`申请的内存。
* 未使用的内存。
* STACK（栈空间）：局部变量、参数、返回值都存在这里，函数调用开始会参数入栈、局部变量入栈；调用结束依次出栈。

其中堆空间和栈空间的大小是可变的，堆空间从下往上生长，栈空间从上往下生长。

由于常量存储在TEXT段中，所有对常量的赋值都将产生`segment fault`异常。

可以认为BSS段中的所有字节都是0。因为未初始化的全局变量、静态变量都在BSS段中， 所以它们都会被初始化为0，同时类的成员变量也会被初始化为0，但编译器不保证局部变量的初始化。

> 在C++中，如果类中有虚函数，那么它就会有一个虚函数表的指针__vfptr，在类对象最开始的内存数据中。之后是类中的成员变量的内存数据。注意要考虑对齐。

[Content origin1](https://harttle.land/2015/07/22/memory-segment.html)|||[Content origin2](https://vites.app/article/dev/8a9fa889.html)|||[Content origin3](https://www.zhihu.com/question/26224882)

[待看](http://chenqx.github.io/2014/09/25/Cpp-Memory-Management/)

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