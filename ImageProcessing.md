## OpenCV
* ## 基本操作
```
img = cv2.imread(r'1.jpg') # 读取图像
cv2.namedWindow("Image",cv2.WINDOW_NORMAL) # 新建一个名字为'Image'的窗口
cv2.imshow("Image", img) # 显示图像
cv2.imwrite('new_img.jpg', img) # 保存图像
cv2.waitKey (0)  
cv2.destroyAllWindows()  
```
* ## 边缘检测
```
edge = cv2.Canny(image, threshold1, threshold2[, edges[, apertureSize[, L2gradient ]]])
```
* ## Harris角探测器
IMG输入图像，应该是灰度和浮动32型
```
gray = cv2.cvtColor(img,cv2.COLOR_BGR2GRAY)
gray = np.float32(gray)
dst = cv2.cornerHarris(gray,2,3,0.04)
#result is dilated for marking the corners, not important
dst = cv2.dilate(dst,None)
# Threshold for an optimal value, it may vary depending on the image.
img[dst>0.01*dst.max()]=[0,0,255] # 映射到图片
```
* ## Shi-tomasi角探测器
找到25个最佳的拐角例子
```
corners = cv2.goodFeaturesToTrack(gray,25,0.01,10)
corners = np.int0(corners)
for i in corners:
    x,y = i.ravel()
    cv2.circle(img,(x,y),3,255,-1)
```
* ## SIFT
```
sift = cv2.xfeatures2d.SIFT_create()
kp = sift.detect(gray,None)
img=cv2.drawKeypoints(gray,kp,img)
#img=cv2.drawKeypoints(gray,kp,img,flags=cv2.DRAW_MATCHES_FLAGS_DRAW_RICH_KEYPOINTS)
```
