### 1.使用assert
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
  
