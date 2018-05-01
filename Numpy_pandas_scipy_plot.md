
## Numpy
#### 基本操作
* 转置：data.transpose()&data.T(list)------list为转置的列下标
* 协方差矩阵：np.cov(data,rowvar=0)------[rowvar=0]------行为特征
* 求平均值：np.mean(data,axis=0)------[axis=0按列]

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

## Matplotlib

* ### Seaborn
```
import seaborn as sns
sns.set()             #切换到seaborn主题
sns.set_context("poster") #设置粗细,分别是paper，notebook, talk, and poster
sns.set_context("notebook", font_scale=1.5, rc={"lines.linewidth": 2.5}) #单独设置
sns.set_palette(sns.color_palette("hls", 6)) #设置颜色主题
```
