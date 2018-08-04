## 画图
* #### 相关显示
```
set(0,'defaultfigurecolor','w')  %全局背景颜色
set(gca,'FontSize',14)           %坐标轴标度字大小
title('Title','fontsize',16)
xlabel('xxxx','fontsize',14)     %横坐标名字大小
```
* #### 控制坐标
```
set(gca,'XLim',[-pi/2 pi])       %坐标轴范围
set(gca,'XTick',[-pi/2:pi/4:pi]) %坐标轴显示步长
set(gca,'XTickLabel',{'-pi/2' '-pi/4:' '0' 'pi/4' 'pi/2' 'pi*3/4' 'pi'});%替换相应步长标签
```
