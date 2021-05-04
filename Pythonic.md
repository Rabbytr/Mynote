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

### numpy.argmin传入map会有问题

### str()&repr()

str()面向用户，repr()面向解释器
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
### 私有成员

Python私有成员`__var`会被映射为`_{class name}__var`

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

### 设置最大迭代深度

```
from sys import setrecursionlimit
setrecursionlimit(maxrecursion)
```

### 元编程

万物皆对象，对象是类的实例，类是元类的实例

`type`就是一个元类，可以通过`type`来实例化一个类

```python
Dog = type('Dog',(object,),{'eat':lambda self:print('Eatting')})
d = Dog()
d.eat()
# output:Eatting
```

使用元类控制类的行为：

```python
class MyMeta(type):
    def __new__(meta,clsname,bases,attrdict):
        return super().__new__(meta,clsname,bases,attrdict)

    def __init__(cls,clsname,bases,attrdict):
        super().__init__(clsname,bases,attrdict)

    def __call__(cls):
        return super().__call__()

    @classmethod
    def __prepare__(meta, clsname, bases):
        return dict()

class dog(metaclass=MyMeta):
    """docstring for dog"""
    def __init__(self):
        super(dog, self).__init__()

d = dog()
```

元类继承自`type`,行为通过实现

- `__new__(meta,name,bases,class_dict)`

  类似于类中的`__new__`,用于定义元类的创建行为

- `__init__(cls, name, bases,attr_dict)`

  类似于类中的`__init__`,用于初始化元类,通过元类产生类时会用到.

- `__call__(cls)`

  定义类实例化时的行为.

- 类方法`__prepare__(meta, name, bases)`

  解释器调用元类的`__new__` 方法之前会先调用`__prepare__` 方法,使用类定义体中的属性创建映射.`__prepare__` 方法的第一个参数是元类,随后两个参数分别是要构建的类的名称和基类组成的元组,返回值必须是映射.元类构建新类时,`__prepare__`方法返回的映射会传给`__new__` 方法的最后一个参数,然后再传给`__init__` 方法.

使用元类的类实例化产出类的顺序是:

1. `meta.__prepare__`
2. `meta.__new__`
3. `meta.__init__`

类实例化对象的顺序是:

1. `cls.__call__`
2. `cls.__new__`
3. `cls.__init__`

#### 描述符

属性访问的默认行为是从一个对象的字典中获取、设置或删除属性。例如，`a.x` 的查找顺序会从 `a.__dict__['x']` 开始，然后是 `type(a).__dict__['x']`，接下来依次查找 `type(a)` 的基类，不包括元类。 如果找到的值是定义了某个描述器方法的对象，则 Python 可能会重载默认行为并转而发起调用描述器方法。这具体发生在优先级链的哪个环节则要根据所定义的描述器方法及其被调用的方式来决定。

```python
descr.__get__(self, obj, type=None) -> value
descr.__set__(self, obj, value) -> None
descr.__delete__(self, obj) -> None
```

访问`__dict__`时会调用`__getattribute__`方法，在重写`__getattribute__`时，使用`object.__getattribute__(self, name)` 或者 `super().__getattribute__(item)` 而不是 `self.__dict__[item]`，当要访问的属性不存在时，会转而调用`__getattr__`

如果一个对象定义了 `__set__()`或 `__delete__()`，则它会被视为**数据描述器**。 仅定义了 `__get__()`的描述器称为**非数据描述器**（它们通常被用于方法，但也可以有其他用途）。

使用非数据描述器，纯 Python 版本的 `staticmethod()`如下所示：

```python
class StaticMethod(object):
    "Emulate PyStaticMethod_Type() in Objects/funcobject.c"

    def __init__(self, f):
        self.f = f

    def __get__(self, obj, objtype=None):
        return self.f
```

使用非数据描述符协议，纯 Python 版本的 `classmethod()` 如下：

```python
class ClassMethod(object):
    "Emulate PyClassMethod_Type() in Objects/funcobject.c"

    def __init__(self, f):
        self.f = f

    def __get__(self, obj, klass=None):
        if klass is None:
            klass = type(obj)
        def newfunc(*args):
            return self.f(klass, *args)
        return newfunc
```

####  上下文管理

*上下文管理器* 是一个对象，它定义了在执行 [`with`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#with) 语句时要建立的运行时上下文。 上下文管理器处理进入和退出所需运行时上下文以执行代码块。 通常使用 `with` 语句（在 [with 语句](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#with) 中描述），但是也可以通过直接调用它们的方法来使用。

列表事物处理的两种上下文管理器写法

```python
from contextlib import contextmanager

@contextmanager
def dec_transaction(orig_list):
    working = list(orig_list)
    yield working
    orig_list[:] = working

class cls_transaction:
    def __init__(self, orig_list):
        self.orig_list = orig_list
        
    def __enter__(self):
        self.working = list(self.orig_list)
        return self.working

    def __exit__(self, exc_type, exc_val, exc_tb):
        if not exc_type:self.orig_list[:] = self.working

a = [1,2,3,4]

with cls_transaction(a) as l:
    l.append(5)
    raise RuntimeError('fdsf')
    l.append(6)

print(a)
```

#### 装饰器

```python
from functools import wraps

def log(n):
    def decorate(func):
        @wraps(func)
        def wrapper(*args,**kwargs):
            print('S'*n)
            result = func(*args,**kwargs)
            print('T'*n)
            return result
        return wrapper
    return decorate

@log(20)
def func():
    print(666)

func()
func.__wrapped__()
```

使用`functools` 的 `wraps` 装饰器能保留函数的元信息，`@wraps` 有一个重要特征是它能让你通过属性 `__wrapped__` 直接访问被包装函数。



### Python特殊属性&方法

见[Python数据模型](https://docs.python.org/zh-cn/3/reference/datamodel.html)

* Python类静态成员在类`__dict__`中
* 访问实例的属性才会调用`__getattribute__`或`__getattr__`

#### `__getattribute__`Python实现

```python
def object_getattribute(obj, name):
    "Emulate PyObject_GenericGetAttr() in Objects/object.c"
    null = object()
    objtype = type(obj)
    cls_var = getattr(objtype, name, null)
    descr_get = getattr(type(cls_var), '__get__', null)
    if descr_get is not null:
        if (hasattr(type(cls_var), '__set__')
            or hasattr(type(cls_var), '__delete__')):
            return descr_get(cls_var, obj, objtype)     # data descriptor
    if hasattr(obj, '__dict__') and name in vars(obj):
        return vars(obj)[name]                          # instance variable
    if descr_get is not null:
        return descr_get(cls_var, obj, objtype)         # non-data descriptor
    if cls_var is not null:
        return cls_var                                  # class variable
    raise AttributeError(name)
```

可见实例查找通过命名空间链进行扫描，优先级从高到低为**数据描述器**，**实例变量**、**非数据描述器**、**类变量**，最后是 `__getattr__()`（如果有）。

如果 `a.x` 找到了一个描述器，那么将通过 `desc.__get__(a, type(a))` 调用它。

属性查找不会直接调用 `object.__getattribute__()`，点运算符和 `getattr()`函数均通过辅助函数执行属性查找：

```python
def getattr_hook(obj, name):
    "Emulate slot_tp_getattr_hook() in Objects/typeobject.c"
    try:
        return obj.__getattribute__(name)
    except AttributeError:
        if not hasattr(type(obj), '__getattr__'):
            raise
    return type(obj).__getattr__(obj, name)             # __getattr__
```

同时，如果用户直接调用 `object.__getattribute__()` ，则 `__getattr__()` 的钩子将被绕开。

