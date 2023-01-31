---
title: Dockerfile syntax
date: 2023-01-31 07:20:37
tags:
---

## Dockerfile là gì?

Dockerfile là gì? Dockerfile là một file dạng text không có phần đuôi mở rộng, chứa các đặc tả về một trường thực thi phần mềm, cấu trúc cho Docker Image. Từ những câu lệnh đó, Docker sẽ build ra Docker image (thường có dung lượng nhỏ từ vài MB đến lớn vài GB).

## Syntax

Trước hết thì mình có example về 1 Dockerfile file dùng để build 1 máy ảo linux có chứa tool tippecanoe

```Dockerfile
# Ver của máy ảo
FROM ubuntu:22.04 
# Các câu lệnh terminal - vì đã lấy được quyền root sẵn khi tạo container nên không cần sudo
RUN apt-get update &&  ACCEPT_EULA=Y 
RUN apt-get install nodejs -y
RUN apt-get install git -y
RUN apt-get install make -y
# Giống cd - change directory
WORKDIR ~
RUN git clone https://github.com/mapbox/tippecanoe.git
WORKDIR tippecanoe/
RUN apt-get install g++ -y
RUN apt-get install build-essential libsqlite3-dev zlib1g-dev -y
RUN make \
    && make install
# Tên user
RUN useradd -ms /bin/bash apprunner
USER apprunner
```