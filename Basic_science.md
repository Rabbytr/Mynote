
## Numpy
#### 基本操作
* 转置：data.transpose()&data.T(list)------list为转置的列下标
* 协方差矩阵：np.cov(data,rowvar=0)------[rowvar=0]------行为特征
* 求平均值：np.mean(data,axis=0)------[axis=0按列]
* 求阶乘：np.math.factorial(k)

## Pandas
* #### Data input
```
data = pd.read_excel('data.xls')
data = pd.pd.read_csv('data.csv')
```
* #### Data output
```
data.to_excel('outdata.xls', sheet_name='sheet1')
data.to_csv('outdata.csv')
```
* #### Data Screen&Slice
```
------选取列------
a = data[['columnname']] #a是DataFrame
b = data['columnname']   #b是Series
------选取行------
a = data[n:m]  #a是DataFrame,选取n到m行，含头不含尾
b = data.loc['indname1':'indname2'] 选取indname1到indname2的行
------选取行和列------
a = data.loc['indname1':'indname2',['columnname']] #返回DataFrame  
b = data.loc['indname1':'indname2','columnname'] #返回Series
用index取数是含头又含尾的
```

## Scipy

## Sympy
* ### 导入
```
from sympy import *
from sympy import pi, E, oo, I # oo为正无穷，同理-oo,I为复数
```
* ### 美观打印表达式
```
from sympy import init_printing
init_printing(use_unicode=False, wrap_line=False, no_global=True)
```
* ### 特性
```
a = Rational(1,2) # a=1/2
Integral(x) # x的积分的表达式
```
* ### 声明变量
```
x = Symbol('x')
var('a:z') # 声明a-z的变量
var('a:6') # 声明a1-a6
```
* ### f为一个表达式
```
f.subs(old,new) # 替换相应值
limit(f,x,x0) # 求极限
diff(f, var) # 求导
diff(f,var,n) # 求高阶导数
integrate(f,var) # 不定积分
integrate(f,(x,0,oo)) # 定积分&广义积分
f.series(x,0,10) # 泰勒展开
summation(f, (i, a, b)) # 求f(i)在a到b的和
f.expand() # 展开
apart(f,x) # 分数分解
together(f) # 分数合并
```
* ### 微分方程
```
f = Function('f')
var('x')
a = f(x).diff(x, x) + f(x) # 微分方程a=0,diff(x,x)几个x几阶导数
dsolve(a)
```
* ### 代数方程
```
solve(f,var) # 求解f=0的解
```
* ### 打印
```
latex(f) # 打印Latex表达式
```

## Matplotlib
* ### Matplotlib.pyplot&pylab
读取图像: pl.imread(path) #无pillow包仅支持png  
显示图像: pl.imshow()

* ### Seaborn
```
import seaborn as sns
sns.set()             #切换到seaborn主题
sns.set_context("poster") #设置粗细,分别是paper，notebook, talk, and poster
sns.set_context("notebook", font_scale=1.5, rc={"lines.linewidth": 2.5}) #单独设置
sns.set_palette(sns.color_palette("hls", 6)) #设置颜色主题
```
