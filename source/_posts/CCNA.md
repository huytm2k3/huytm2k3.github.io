---
title: CCNA
date: 2022-10-03 08:44:46
tags: [networking]
---

## Mạng là gì

Hai máy tính kết nối với nhau thông qua sợi dây cap, hoặc 2 smartphone kết nối qua bluetooth được gọi là 1 hệ thống mạng, vì chúng có thể kết nối, trao đổi dữ liệu với nhau.

Với hệ thống mạng doanh nghiệp thì phức tạp hơn.

![](/images/CCNAPost/Screenshot_1.png)

Nếu 2 máy tính kết nối với nhau, chúng ta không cần tới switch. Nếu 3 máy tính với nhau, chúng ta vẫn có thể lắp thêm card mạng để kết nối thành hình tam giác, nhưng nếu 4 hoặc nhiều hơn thế nữa, thực sự không khả thi. Vì vậy chúng ta cần dùng tới switch:

![](/images/CCNAPost/Screenshot_2.png)

Để giảm thiệu thiệt hại tấn công mạng - dễ quản lý hơn chúng ta nên chia vùng mạng lớn thành nhiều vùng mạng nhỏ bằng router. Chức năng của Router là để chia vùng mạng.

## Các yếu tố ảnh hưởng đến tốc độ của hệ thống mạng

Các đặc điểm của hệ thống mạng:
- Tốc độ
- Chi phí
- Độ bảo mật
- Độ sẵn sàng
- Khả năng mở rộng
- Độ tin cậy
- Mô hình Topology

Các vấn đề ảnh hưởng tới tốc độ mạng:

- Dây cab phải phù hợp
- Tốc độ mạng của thiết bị đầu cuối
- Switch/Router phù hợp

Trước khi Server gửi dữ liệu cho thiết bị đầu cuối, Server đọc dữ liệu từ RAM.

Cải thiện:

- Sử dụng kĩ thuật RAID (Đọc cùng lúc 4 ổ cứng)
- Trang bị cho server nhiều RAM

Mạng không dây tốc độ mạng không bằng có dây.

Khi mà Film Server giới hạn tốc độ tải dữ liệu về, người dùng thường tải rất chậm. Khi sử dụng IDM thì tải nhanh gấp 4 5 lần.
Lý do là IDM gửi cùng lúc nhiều phiên kết nối tới Film Server và sau đó ghép các mảnh dữ liệu thành file hoàn chỉnh cho người dùng sử dụng. 

## Chi phí - Security

* Chi phí đầu tư Server, hệ thống lưu trữ: Khoản kinh phí đầu tư nhiều nhất, ảnh hưởng nhiều tới quá trình vận hành và các chi phí bảo trì, bảo dưỡng khác.
* Chi phí bảo mật (Security): Cài đặt, sử dụng phần mềm diệt virus uy tín, cập nhật thường xuyên bản vá mới, trang bị các switch bảo mật (hữu dụng), Fillwall.

## Độ sẵn sàng

Nếu thuê 1 kết nối Internet của Viettel, nếu gặp sự cố thì toàn sự cố mạng bị cô lập. Thông thường chúng ta nên thuê 2 nhà cung cấp để có thể dễ dàng chuyển đổi khi 1 trong 2 nhà mạng bị mất kết nối.

## Khả năng mở rộng

Nên chọn thiết bị tốt ngay từ đầu để có khả năng mở rộng thêm người dùng thay vì việc phải thay thế thiết bị mới.

## Độ tin cậy

Không nên sử dụng FPT mà sử dụng sFPT để mã hóa dữ liệu an toàn trước nguy cơ bắt dữ liệu hệ thống.

## Các loại mô hình Topology của hệ thống mạng

![](/images/CCNAPost/Screenshot_2.png)

- Bus Topology: Không bảo mật!
- Ring Topology: Dữ liệu di chuyển theo dạng vòng, mất thời gian.
- Star Topology: Khuyên dùng, được sử dụng phổ biến nhất.

Mặc dù Star Topology có nhiều ưu điểm, nhưng nếu điểm chính giữa gặp sự cố, mọi thiết bị đều bị cô lập. Để khắc phục người ta phát triển thành mô hình Extended Star Topology:

![](/images/CCNAPost/Screenshot_3.png)

Mô hình đặc biệt khác: Full-Mesh Topology và Partial-Mesh

![](/images/CCNAPost/Screenshot_4.png)

## Tổng quan về mô hình OSI

Tất cả các thiết bị máy tính của các hãng khác nhau đều có thể cùng kết nối với nhau là do thông qua mô hình chuẩn hóa OSI. Chỉ cần nắm rõ mô hình OSI là có thể vận hành dễ dàng 1 hệ thống mạng có nhiều loại thiết bị.

Hai máy tính A và B muốn giao tiếp với nhau phải sử dụng cùng ngôn ngữ (IPv4 hoặc IPv6)
Hiện nay tất cả các thiết bị kết nối Internet đều sử dụng chồng giao thức TCP/IP.

Lợi ích của mô hình OSI:
- Giảm thiểu độ phức tạp.
- Chia công việc, dễ dàng quản lý.
- Khắc phục sự cố hệ thống.

### Chức năng của từng lớp

#### 1. Physical

- Môi trường truyền dẫn là Cab - Chuẩn hóa vấn đề liên quan tới vật lý.
- Dưới 100m nên dùng cab đồng, trên 100m dùng cab quang.

#### 2. Data link

- Ethernet, PPPoE, PPP, HDLC, MPLS, Frame Relay.
- Công nghệ Ethernet là phổ biết nhất.

#### 3. Network

Chức năng:
- Định tuyến gói tin
- Tối ưu đường đi
- Quy định cấu trúc - định dạng của địa chỉ IP

#### 4. Transport

- Cung cấp cơ chế điều khiển luồng, điều khiển lỗi
- Cung cấp phương thức truyền thông dữ liệu theo thời gian thực

2 Cơ chế truyền thông phổ biển: UDP, TCP.

UDP gửi 1 loạt tất cả các Segments cùng 1 lúc
TCP gửi từng Segment, khi client gửi lại ACK, TCP mới gửi Segment tiếp theo. Trong một khoảng thời gian xác định, Server không nhận được ACK từ Client, Server sẽ tự gửi lại Segment lỗi đó cho tới khi nhận được ACK từ Client.

#### 5. Session


Chia tài nguyên card mạng, cho phép nhiều ứng dụng truy cập mạng cùng 1 máy.

#### 6. Presentation

Chuyển đổi quá trình truyền thông dữ liệu.

#### 7. Application

Tùy vào từng ứng dụng, ta lại dùng các giao thức khác nhau.

## Mô hình TCP/IP

Bên cạnh OSI, ta còn mô hình chuẩn hóa khác là TCP/IP

Mô hình TCP/IP có 4 phân lớp:
- Application
- Transport
- Internet
- Network Access

![](/images/CCNAPost/Screenshot_6.png)

## Phân tích quá trình đóng gói Encapsulation và giải đóng gói Decapsulation

### Encapsulation

![](/images/CCNAPost/Screenshot_7.png)

### Decasulation

![](/images/CCNAPost/Screenshot_8.png)

## Mối tương quan giữa địa chỉ MAC và địa chỉ IP

Trên hệ thống mạng Ethernet/Lan, mỗi thiết bị được định danh bằng địa chỉ MAC, mỗi card mạng sở hữu 1 địa chỉ MAC. Địa chỉ MAC là duy nhất trên toàn thế giới.





