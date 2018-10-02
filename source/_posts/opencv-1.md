title: 【日常学习】------ Opencv(Python版)-1
date: 2018-10-01 18:23:00
categories:
- Opencv
tags:
- opencv
- python
---
## 摘要
> 了解opencv基本函数功能
<!-- more -->

### 在窗口显示图像
```python
import cv2

img = cv2.imread('sea.jpg')
cv2.imshow('image',img)
cv2.waitKey()
cv2.destroyWindow()
```

### 在窗口显示摄像头帧
> Opencv的namedWindow(),imshow(),DestroyWindow()函数允许指定窗口名来创建，显示和销毁窗口。
> waitKey()函数来获取键盘输入，通过setMouseCallback()函数来获取鼠标输入。以下代码用来打开摄像头，实时显示摄像头帧。

 
```python
import cv2

clicked = False
def onMouse(event, x, y, flags, param):
    global clicked
    if event == cv2.EVENT_LBUTTONUP:
        clicked = True

cameraCapture = cv2.VideoCapture(0)
cv2.namedWindow('MyWindow')
cv2.setMouseCallback('MyWindow',onMouse)

print('Showing camera feed. Click window or press any key to stop')
success, frame = cameraCapture.read()
while success and cv2.waitKey(1) == -1 and not clicked:
    cv2.imshow('MyWindow',frame)
    success, frame = cameraCapture.read()

cv2.destroyWindow('MyWindow')
cameraCapture.release()
```

> 下面这个代码也是打开摄像头并显示帧，按下esc关闭窗口


```python
import cv2
import numpy as np
import pickle
import matplotlib.pyplot as plt

cap = cv2.VideoCapture(0)

while True:
    ret, frame = cap.read()
    # Our operations on the frame come here
    frame = cv2.GaussianBlur(frame, (3, 3), 0)
    frame = cv2.Canny(frame, 70, 200)
    #frame = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    # Display the resulting frame
    cv2.imshow('frame', frame)
    if cv2.waitKey(1) & 0xFF == 27:
        break

# When everything done, release the capture
cap.release()
cv2.destroyAllWindows()
```

> **frame = cv2.GaussianBlur(frame, (3, 3), 0)**,这条代码的意思是对获得的帧加一个高斯模糊，使图像更加平滑。
![my](https://raw.githubusercontent.com/Ryanlzz/Ryanlzz.github.io/master/image/my.jpg)
> **frame = cv2.Canny(frame, 70, 200)**，这条代码的作用是对图像进行边缘检测。
![canny](https://raw.githubusercontent.com/Ryanlzz/Ryanlzz.github.io/master/image/canny.png) 
> **frame = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)**，使图像转变为灰度图像。
![gray](https://raw.githubusercontent.com/Ryanlzz/Ryanlzz.github.io/master/image/mygray.png) 