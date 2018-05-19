
## Numpy
#### 基本操作
* 转置：data.transpose()&data.T(list)------list为转置的列下标
* 协方差矩阵：np.cov(data,rowvar=0)------[rowvar=0]------行为特征
* 求平均值：np.mean(data,axis=0)------[axis=0按列]
* 求阶乘：np.math.factorial(k)
* 卷积运算: np.convolve(a,b)

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

## Networkx
* #### 构建网络
* 建立一个空图
```
import networkx as nx
G=nx.Graph()     #建立一个空图
G=nx.DiGraph()   #建立一个有向空图
```
* 为网络添加节点
```
G.add_node(a point)       #给网络添加节点
G.add_nodes_from(a list)  #给网络添加节点
```
* 为网络添加边
```
G.add_edge(a tuple)        #给网络添加边
G.add_edges_from(a list<tuple>)  #给网络添加边
```
* #### 网络可视化
```
f = figure(1)
nx.draw_networkx(G, pos=None, arrows=True, with_labels=True, **kwds)
```
设置图片背景颜色
```
pl.axis('off')
f.set_facecolor('c')
```  

|参数|作用|
|:--:|:--:|
|G|一个网络图|
|pos|图像的布局，可选择参数；如果是字典元素，则节点是关键字，位置是对应的值。如果没有指明，则会是spring的布局|
|arrows|布尔值，默认True; 对于有向图，如果是True则会画出箭头|
|with_labels|布尔值，默认为True; 如果为True，则在节点上标注标签|
|ax|坐标设置，可选择参数,依照设置好的Matplotlib坐标画图|
|nodelist|一个列表，默认G.nodes(); 给定节点|
|edgelist|一个列表，默认G.edges();给定边|
|node_size|向量或者标量，默认300;表示节点的数目，必须和nodelist长度保持一致|
|node_color|颜色字符串，默认’r’;可以是单个颜色，也可以是和nodelist长度相等的一列颜色字符串|
|node_shape|字符串，默认’o’;节点的形状|
|alpha|浮点数，默认1;节点或者边的透明度|
|cmap|Matplotlib的颜色映射，默认None; 用来表示节点对应的强度|
|vmin,vmax|浮点数，默认None;节点颜色映射尺度的最大和最小值|
|linewidths|[None-标量-一列值];节点边界的线宽|
|width|浮点数，默认1;边的的线宽|
|edge_color|颜色字符串，默认’r’;边的颜色，可以是一个颜色值，也可以是一列颜色值，如果是一列颜色值，其长度必须和edgelist的长度保持一致|
|edge_cmap|	Matplotlib的颜色映射，默认None; 用来表示边对应的强度|
|edge_vmin,edge_vmax|	浮点数，默认None;边的颜色映射尺度的最大和最小值|
|style|默认’solid’; 边的线的风格，可以是 soldid，dashed， dotted，dashdot|
|labels|字典元素，默认None;文本形式的节点标签|
|font_size|整型，默认None; 文本标签的字体大小|
|font_color|字符串，默认’k’(黑色)|
|font_weight|字符串，默认’normal’|
|font_family|字符串，默认’sans-serif’|

* [Networkx文档](https://networkx.github.io/documentation/networkx-1.10/reference/introduction.html)
