---
title: CompTIA Network
date: 2022-09-20 07:26:50
tags:
---
# Hiểu mô hình OSI là gì?
Mô hình OSI là viết tắt của Open Systems Interconnection Reference Model, được chia thành 7 tầng:
- Tầng vật lý (Physical layer):
Giao tiếp giữa các phần mạng bằng Cab, Cab quang. Nếu có vấn đề về tầng vật lý, thường thấy chúng ta sẽ kiểm tra lại dây Cab, Adapter Card.
- Tầng liên kết dữ liệu (Data-Link layer):
Phương thức điều khiển: Địa chỉ MAC (Media Access Control) trên Ethernet
Có thể coi nó như tầng "chuyển đổi"
- Tầng mạng (Network Layer):
Tầng định tuyến
Internet Protocol (IP)
- Tầng vận chuyển (Transport Layer):
Có thể gọi là "post office" layer: Vận chuyển bưu kiện, thư từ.
Phương thức: TCP (Transmission Control Protocol) và UDP (User Datagram Protocol)
- Tầng phiên (Session layer):
Quản lý giao tiêm giữa các thiết bị: Start, stop, restart
Control protocols, tunneling protocols
- Tầng trình bày (Presentation layer):
Mã hóa ký tự
Mã hóa ứng dụng
Kết hợp với Tầng ứng dụng
- Tầng ứng dụng (Application layer):

# WAN Termination


## Demarcation point

Điểm phân chia ranh giới kết nối của bạn với thế giới bên ngoài

- WAN provider
- Nhà cung cấp dịch vụ Internet
- Demarc

Sử dụng ở mọi nơi

- Ở nhà

Vị trí trung tâm của 1 toà nhà

RJ-45 connection

## Smartjack

NIU (Network interface unit)

- Thiết bị xác định ranh giới
- Thiết bị giao diện mạng, giao diện mạng điện thoại

Smartjack

Chẩn đoán tích hợp

- Loopback tests

