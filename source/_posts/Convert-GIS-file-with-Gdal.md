---
title: Convert GIS file with Gdal
date: 2022-04-21 08:18:35
tags:
---
## Mở đầu

Phần lớn những file GIS như *.kml, *.shp, *.dbf, *.prj có thể kéo vào QGIS để sử dụng, nhưng để có thể hiển thị được trên mapbox bắt buộc server phải convert về file geoJson.
Để làm được điều đó chúng ta sẽ sử dụng Gdal.

## Installation

Source: https://sandbox.idre.ucla.edu/sandbox/tutorials/installing-gdal-for-windows

### Step 1: Install Python

Download: https://www.python.org/

Sau đó, vào Start, tìm kiếm Python. Mở lên và kiểm tra phiên bản
![](/images/GdalPost/Screenshot_1.png)
![](/images/GdalPost/Screenshot_2.png)

### Step 2: Install GDAL

Truy cập: https://www.gisinternals.com/release.php

Chọn phiên bản phù hợp với Python version
![](/images/GdalPost/Screenshot_3.png)

Sau đó tải 2 thứ này: 
![](/images/GdalPost/Screenshot_4.png)

### Step 3: Set environment variables (Cài đặt biến môi trường)
Nếu chưa biết biến môi trường là gì và hoạt động ra sao, truy cập vào Post: http://huytm2k3.github.io/2022/03/30/Tim-hieu-ve-bien-moi-truong-trong-windows/

Vào Start, gõ Environment
![](/images/GdalPost/Screenshot_5.png)
Tìm tới "Path" Ở System Variables
![](/images/GdalPost/Screenshot_6.png)
![](/images/GdalPost/Screenshot_7.png)
Thêm vào cuối: C:\Program Files (x86)\GDAL
![](/images/GdalPost/Screenshot_8.png)

Tạo thêm 1 biến môi trường GDAL_DATA với value: C:\Program Files (x86)\GDAL\gdal-data
![](/images/GdalPost/Screenshot_9.png)
### Step 4: Kiểm tra
Mở Command line (Ở window là Command prompt hoặc PowerShell)
```bash
gdalinfo --version
```
Thành công: 
![](/images/GdalPost/Screenshot_10.png)