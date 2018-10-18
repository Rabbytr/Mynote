### 使用assert
```
x = 1
y = 2
assert x == y,'not equals'
```
python -O xxx.py 可以禁用断言(注意O大写)

### 用isinstance()而不是type()做类型检测
```
isinstance(3,(int,float,str))
```
### 用enumerate(list,start=1)获取序列迭代索引和值
```
li = ['a','b','c','d','e']
for i,e in enumerate(li):
    print(i,e)
```
### 使用with自动关闭资源
```
with open('a.txt','w') as f:
    f.write('text')
```
### 优先使用join而不是+
```
''.join([str1,str2,str3])
```
### 优先使用.format而不是%
基本语法{varname:[**填充符**][**对齐方式**][**符号**][**宽度**][**,**][**.精度**][**转换类型**]}
###### 对齐方式
* <&> 左对齐&右对齐
* = 符号左对齐数值右对齐(仅对数值有效)
* ^ 居中对齐  

###### 符号
* 【\+】     正数前+，负数前-
* 【\-】     默认
* 【空格】   正数前空格，负数前-
```
print("start{g:*^+30,.2f}end".format(g=123456.789))
```

### 默认参数尽量默认None,函数内部动态生成
默认参数在函数被调用时仅仅被评估一次，以后都会使用第一次评估的结果
### str()&repr()
str()面向用户，repr()面向解释器
### \_\_init\_\_()不是构造函数
\_\_new\_\_才是
### 操作符重载
重载<<操作符
```
class cout(object):
    def __lshift__(self,obj):
        if obj is 'endl':
            print()
            return
        print(obj)
        return self
```
### 使用生成器提高效率
斐波那契数列
```
def fib(n):
    a = b = 1
    for i in range(n):
        yield a
        a,b = b,a+b
f = fib(10)
a = next(f)
```
### 自定义比较器
functools库中提供了一个装饰器 total_ordering  
只需要实现 __eq__ 方法和其他任意一个方法就可以实现cmp.
```
from functools import total_ordering

@total_ordering
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    def __eq__(self, other):
        return (self.x, self.y) == (other.x, other.y)

    def __lt__(self, other):
        return (self.x, self.y) < (other.x, other.y)
```

### for...else...
for...else...的else部分用来处理没有从for循环中断的情况。
有了它，我们不用设置状态变量来检查是否for循环有break出来，简单方便。

### 设置最大迭代深度
```
from sys import setrecursionlimit
setrecursionlimit(maxrecursion)
```
