## OpenCV
* ### 基本操作

```
# 读取图像
img = cv2.imread(r'1.jpg')
# 新建一个名字为'Image'的窗口
cv2.namedWindow("Image",cv2.WINDOW_NORMAL)
# 显示图像
cv2.imshow("Image", img)
# 保存图像
cv2.imwrite('new_img.jpg', img)

cv2.waitKey (0)  
cv2.destroyAllWindows()  
```
