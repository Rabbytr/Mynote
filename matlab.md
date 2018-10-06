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

## Image Processing
## 基本读写
```
img = imread('peppers.png'); % 读取图片
imwrite(gray,'test.png');    % 保存图片
```
## 灰度变化
```
gray = rgb2gray(img);        % 灰度化
J = histeq(gray);            % 直方图均衡化
```
## 显示
```
imshow(img);
image(img);                  % 显示图片
imhist(gray);                % 显示直方图
```
