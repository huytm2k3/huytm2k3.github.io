---
title: Deploy with Ubuntu (ssh)
date: 2022-04-21 14:47:08
tags:
---


## How to edit file config *.conf in Ubuntu
Trong /etc/nginx/conf.d sẽ chứa những file config.
Để sửa những file này, ta cần dùng tới vim hoặc nano, ... và cần dùng tới quyền root.

Root:
```
sudo -i
```
cd tới thư mục chứa file config.

và dùng:

```
nano <fileName>
```
## Save file with nano

Ctrl + S

## Kiểm tra cú pháp nginx

```
nginx -t
```
Và reload nginx
```
nginx -s reload
```