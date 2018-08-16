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
* ## 图片变换
```
img = cv2.flip(img,0) # 垂直翻转
img = cv2.flip(img,1) # 水平翻转
```
* ## 图片灰度化
```
gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
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

## 视频处理
### 捕获视频
```
cap = cv2.VideoCapture(0)

# 关闭
cap.release()
# cv2.destroyAllWindows()
```
若传入视频文件路径则读取视频文件，若传入数字比如0，则读取计算机的第一个摄像头
### 视频参数
```
prop = cap.get(propId) # 得到视频的一项参数
cap.set(propId,value)  # 设置参数
```
propId具体如下(顺序对应Id):  
![propId](./imgs/propId.png)
### 得到视频每一帧
```
while(cap.isOpened()):
    ret, frame = cap.read()
    if ret == true:

        #tackle per frame

        if cv2.waitKey(1) & 0xFF == ord('q'):
            break
    else:
        break
```
### 保存视频
```
width = int(cap.get(3))
height = int(cap.get(4))
fps = int(cap.get(5))

fourcc = cv2.VideoWriter_fourcc(*'XVID')
out = cv2.VideoWriter('output.mp4',fourcc, fps, (width,height))

while(cap.isOpened()):
    ret, frame = cap.read()
    if ret == true:
        out.write(frame)
        if cv2.waitKey(1) & 0xFF == ord('q'):
            break
    else:
        break
cap.release()
out.release()
cv2.destroyAllWindows()
```
