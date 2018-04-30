
## Numpy
#### 基本操作
* 转置：data.transpose()&data.T(list)------list为转置的列下标
* 协方差矩阵：np.cov(data,rowvar=0)------[rowvar=0]------行为特征
* 求平均值：np.mean(data,axis=0)------[axis=0按列]

## Pandas

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
