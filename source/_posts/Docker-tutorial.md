---
title: Docker tutorial
date: 2022-12-23 13:25:28
tags:
---

## Docker là gì? Tại sao lại cần Docker?
Docker là một dự án mã nguồn mở giúp tự động triển khai các ứng dụng Linux và Windows vào trong các container ảo hóa. Docker cung cấp một lớp trừu tượng và tự động ảo hóa dựa trên Linux.
Docker dùng để đóng gói phần mềm, mã nguồn giúp khách hàng - người dùng gom và cài đặt và sử dụng sản phẩm một cách dễ dàng hơn mà không cần phải cài đặt nhiều gói tài nguyên cần thiết.
http://docker.com
## Getting started với Docker Desktop - Chuẩn bị môi trường cho Docker
Source: http://docker.com/get-started

```bash
docker run -d -p 80:80 docker/getting-started
```

Chạy dự án ở local:

Clone project getting-started
```bash
git clone https://github.com/docker/getting-started.git
```

Change dir tới thư mục ./app

```bash
cd app
```

Tạo file Dockerfile để config build cho Docker:

```Dockerfile
# syntax=docker/dockerfile:1
FROM node:16-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
EXPOSE 3000
```
Build:
```bash
docker build -t getting-started .
```

Run:

```bash
docker run -dp 3000:3000 getting-started
```

## Update Application

1. Lấy danh sách ID của các container

```bash
docker ps
```

2. Dừng container cũ

```bash
docker stop <id>
```

3. Xóa container

```bash
docker rm <id>
```

4. Run container mới

```bash
docker run -dp 3000:3000 getting-started
```

## Share Application

https://docs.docker.com/get-started/04_sharing_app/


## Ubuntu container

Tạo mới 1 ubuntu container:

```bash
docker run -i -t ubuntu
```

Kill 1 ubuntu container:

```bash
docker run <container_id>
```

Start 1 ubuntu container đã stop:

```bash
docker start <container_id>
```

Start 1 ubuntu với command line:

```bash
docker start -ai <container_id>
```
