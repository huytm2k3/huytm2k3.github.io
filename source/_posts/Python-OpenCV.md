---
title: Python OpenCV
date: 2022-10-10 09:11:38
tags:
---

## OpenCV là gì

OpenCV là một thư viện các chức năng lập trình chủ yếu nhắm vào thị giác máy tính thời gian thực. Ban đầu được phát triển bởi Intel, sau đó nó được hỗ trợ bởi Willow Garage sau đó là Itseez. Thư viện đa nền tảng và được sử dụng miễn phí theo Giấy phép Apache 2 nguồn mở.

## Cài đặt

https://docs.opencv.org/4.x/da/df6/tutorial_py_table_of_contents_setup.html

## Gui Features

### Images

Đọc, ghi hình ảnh

```python
import cv2 as cv
import sys

img = cv.imread(cv.samples.findFile("299120506_847557516606630_3970779881691298699_n.jpg"))

# Kiem tra xem co doc duoc hinh anh hay khong

if img is None:
    sys.exit("Could not read the image.")

# Neu doc duoc hinh anh, hien thi len man hinh

cv.imshow("Display window", img)

# Dung chuong trinh lai cho toi khi user bam 1 nut

k = cv.waitKey(0)

# Tao tep hinh anh neu bam phim S

if k == ord("s"):
    cv.imwrite("299120506_847557516606630_3970779881691298699_na.jpg", img)
```

### Videos

#### Capture Video from Camera

```py
import numpy as np
import cv2 as cv
cap = cv.VideoCapture(0)
if not cap.isOpened():
    print("Cannot open camera")
    exit()
while True:
    # Capture frame-by-frame
    ret, frame = cap.read()
    # if frame is read correctly ret is True
    if not ret:
        print("Can't receive frame (stream end?). Exiting ...")
        break
    # Our operations on the frame come here
    gray = cv.cvtColor(frame, cv.COLOR_BGR2GRAY)
    # Display the resulting frame
    cv.imshow('frame', gray)
    if cv.waitKey(1) == ord('q'):
        break
# When everything done, release the capture
cap.release()
cv.destroyAllWindows()
```

#### Play video from file
```python
import numpy as np
import cv2 as cv
cap = cv.VideoCapture('video-2fff691a-baa3-4e06-99d2-adc8de6d03a7-1665324752.mp4')
while cap.isOpened():
    ret, frame = cap.read()
    # if frame is read correctly ret is True
    if not ret:
        print("Can't receive frame (stream end?). Exiting ...")
        break
    gray = cv.cvtColor(frame, cv.COLOR_BGR2GRAY)
    cv.imshow('frame', gray)
    if cv.waitKey(1) == ord('q'):
        break
cap.release()
cv.destroyAllWindows()
```

#### Saving a video

```python
import numpy as np
import cv2 as cv
cap = cv.VideoCapture(0)
# Define the codec and create VideoWriter object
fourcc = cv.VideoWriter_fourcc(*'XVID')
out = cv.VideoWriter('output.avi', fourcc, 20.0, (640,  480))
while cap.isOpened():
    ret, frame = cap.read()
    if not ret:
        print("Can't receive frame (stream end?). Exiting ...")
        break
    frame = cv.flip(frame, 0)
    # write the flipped frame
    out.write(frame)
    cv.imshow('frame', frame)
    if cv.waitKey(1) == ord('q'):
        break
# Release everything if job is finished
Qcap.release()
out.release()
cv.destroyAllWindows()
```

### Drawing Function

https://docs.opencv.org/4.x/dc/da5/tutorial_py_drawing_functions.html

Paint Brush App:

```py
import numpy as np
import cv2 as cv
drawing = False # true if mouse is pressed
mode = True # if True, draw rectangle. Press 'm' to toggle to curve
ix,iy = -1,-1
# mouse callback function
def draw_circle(event,x,y,flags,param):
    global ix,iy,drawing,mode
    if event == cv.EVENT_LBUTTONDOWN:
        drawing = True
        ix,iy = x,y
    elif event == cv.EVENT_MOUSEMOVE:
        if drawing == True:
            if mode == True:
                cv.rectangle(img,(ix,iy),(x,y),(0,255,0),-1)
            else:
                cv.circle(img,(x,y),5,(0,0,255),-1)
    elif event == cv.EVENT_LBUTTONUP:
        drawing = False
        if mode == True:
            cv.rectangle(img,(ix,iy),(x,y),(0,255,0),-1)
        else:
            cv.circle(img,(x,y),5,(0,0,255),-1)
img = np.zeros((512,512,3), np.uint8)
cv.namedWindow('image')
cv.setMouseCallback('image',draw_circle)
while(1):
    cv.imshow('image',img)
    k = cv.waitKey(1) & 0xFF
    if k == ord('m'):
        mode = not mode
    elif k == 27:
        break
cv.destroyAllWindows()
```

### More Advanced Features

https://docs.opencv.org/4.x/d3/df2/tutorial_py_basic_ops.html: 
- Truy cập và sửa đổi giá trị pixel
- Truy cập thuộc tính hình ảnh
- Image ROI
- Tách và hợp nhất hình ảnh
- Tạo viền cho hình ảnh

