---
title: Python Django
date: 2022-11-01 09:59:40
tags:
---

## Yêu cầu

Cài đặt Python, add biến môi trường.
IDE, ở đây tôi sử dụng Visual Studio Code

## Cài đặt

Với Window:

```bash
python -m pip install Django
```

Với Linux:

```bash
sudo apt-get install python3 python-django
```

## Getting Started

### Khởi tạo dự án

```bash
django-admin startproject <Tên Project>
```

cd tới thư mục dự án và mở IDE Visual Studio Code

### Chạy dự án

```bash
python manage.py runserver
```

Khi này dự án được chạy tại http://localhost:8000

### Đổi PORT

```bash
python manage.py runserver <PORT mới>
```

## Tạo WebApp

```bash
python manage.py startapp <ten app>
```

Sau đó cập nhật setting lại

```bash
python manage.py migrate
```

## Tạo Response trang chủ

Bước 1: Tạo WebApp với tên là home

```bash
python manage.py startapp home
```

Cập nhật setting:

```bash
python manage.py migrate
```

Bước 2: Chỉnh sửa file ./home/views.py

```python
from django.shortcuts import render
from django.http import HttpResponse

# Create your views here.

def index(request):
    response = HttpResponse()
    response.writelines("<h1>Xin chao</h1>")
    response.write("Đây là App Home")
    return response
```

Bước 3: Set URL cho trang ở App Home

Tạo và sửa file urls.py trong thư mục home

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index)
]
```

Bước 4: Set URL ở thư mục chính Project

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('home/', include('home.urls'))
]
```

## Test case

Ở tests.py, có thể tạo các test cases

```python
from django.test import TestCase, SimpleTestCase

# Create your tests here.
class SimpleTests(SimpleTestCase):
    def test_home_page_status(self):
        response = self.client.get('/')
        self.assertEquals(response.status_code, 200)
```

Và
```bash
python manage.py test home
```

## Template và Jinja

Không khó lắm, khá giống component trong React

https://www.youtube.com/watch?v=p1q39gPvDAI&list=PL33lvabfss1z8GYxjyMulCnhcYGk5ah8P&index=4

Có thể dùng lại các component với content khác nhau.




