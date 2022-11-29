---
title: Lý thuyết kiến trúc Node.js
date: 2022-11-29 14:38:12
tags:
---

Bài viết này được mình gom góp từ nhiều nguồn khác nhau trên Internet, chia sẻ cho mọi người kiến thức về kiến trúc Node.js một cách dễ hiểu và đầy đủ nhất cũng như ôn luyện cho phỏng vấn 2023 luôn.

## NodeJS là gì

NodeJS là một môi trường runtime chạy JavaScript đa nền tảng và có mã nguồn mở, được sử dụng để chạy các ứng dụng web bên ngoài trình duyệt của client. Nền tảng này được phát triển bởi Ryan Dahl vào năm 2009, được xem là một giải pháp hoàn hảo cho các ứng dụng sử dụng nhiều dữ liệu nhờ vào mô hình hướng sự kiện (event-driven) không đồng bộ.

## V8

Node.js được xây dựng trên V8 engine của Google. Nó là công cụ javascript nhanh nhất. V8 engine chuyển đổi code javascript thành mã máy mà máy tính thực sự hiểu được. Kết quả sau đó được tạo và trả về node.js. Node.js không thể hiểu mã javascript mà chúng ta viết mà không có V8. Bên cạnh javascript, V8 cũng sử dụng C ++.

## I/O bất đồng bộ

NodeJS sử dụng cơ chế bất đồng bộ, có nghĩa là như nào?

Với I/O đồng bộ, 1 Thread sẽ đợi cho đến khi toàn bộ hành động kết thúc, có nghĩa là chuỗi các lệnh sẽ đợi nhau kết thúc để thực thi tới bước tiếp theo. Còn với bất đồng bộ, I/O sẽ chạy ở chế độ nền, không đợi nhau và sẽ được gọi khi kết thúc. I/O bất đồng bộ giúp chương trình hoạt động trơn tru, nhanh hơn mà không bị nghẽn.

## LIBUV

Một dependency node.js được viết bằng C++, triển khai 2 tính năng quan trọng là Event loop và Thread pool

## Event Loop

Event Loop được coi là trái tim của Node.js, nó làm cho Node hoàn toàn khác biệt với các ngôn ngữ Back end khác.

Phần này khá khó hiểu và rắc rối, nên mình sẽ tách ra thành 1 bài riêng.

## Thread pool

Thread pool xử lý các tác vụ nặng nên cung cấp cho chúng ta 4 thread bổ sung hoàn toàn tách biệt với single thread trong Event loop. Event loop sẽ tải bớt các tác vụ nặng vào Thread pool và điều này diễn ra tự động. Một số tác vụ tốn kém được giảm tải là:  tất cả các hoạt động xử lý tệp, mọi thứ liên quan đến mật mã, như mật khẩu lưu vào bộ nhớ đệm, sau đó là tất cả các hoạt động liên quan đến nén, tra cứu DNS (khớp các miền web với địa chỉ IP thực tương ứng của chúng) và hơn thế nữa.
