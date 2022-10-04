---
title: Kinh nghiệm CTF
date: 2022-10-04 08:37:05
tags: [ctf]
---

## Các trang web hữu dụng

Trang web chuyển đổi mã nhị phân, mã HEX, ...: https://kt.gy/tools.html#conv/

## Các câu lệnh Terminal của Kali linux

```cmd
nc <url> <port> # Netcat
wget <url> # Tải và lưu file
strings <ten_file> # Lấy dữ liệu dạng văn bản từ file
strings <ten_file> | grep <noi_dung> # Tìm kiếm văn bản từ file
ssh <url> # Remote máy chủ
cat <file_name> # Đọc file txt
grep <content> * # Tìm kiếm chuỗi content từ tất cả các file trong cùng thư mục và thư mục con
exiftool <ten_file_anh> # Xem chi tiết file ảnh (License có thể decode)
```

## Kinh nghiệm

- Một số file hình ảnh chứa những thuộc tính (License, ..) mã base, decode sẽ được flag.
- Một số file zip được ẩn giấu dưới dạng file hình ảnh, nên ta có thể unzip để xem những file ẩn trong nó.
