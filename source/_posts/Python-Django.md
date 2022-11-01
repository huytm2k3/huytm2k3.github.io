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