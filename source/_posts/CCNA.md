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

![](/images/CCNAPost/Screenshot_9.png)

Trước đây, các thiết bị giao tiếp hoàn toàn bằng MAC.

## Kích thước tối đa của một Segment

![](/images/CCNAPost/Screenshot_10.png)

## Cơ chế hoạt động của UDP và TCP

TCP trải qua quá trình bắt tay 3 bước mới tiếp tục truyền dữ liệu, gửi từng Segment và đợi phản hồi ACK mới truyền tiếp nên có khả năng phục hồi dữ ljeieu
UDP không có khả năng phục hồi dữ liệu - gửi dữ liệu một cách ồ ạt.

## Cơ chế điều khiển luồng Flow Control trong giao thức UDP

## Xác định địa chỉ MAC của máy tính sử dụng HĐH Windows

### Cách 1

Bước 1: Windows + R, Gõ ncpa.cpl -> Enter
Bước 2: Chuột phải Ethernet, chọn Status
Bước 3: Địa chỉ MAC là hàng Physical address

### Cách 2

Mở Command line, gõ ipconfig /all

## Phân tích quá trình trao đổi dữ liệu giữa các thiết bị trong hệ thống mạng LAN

![](/images/CCNAPost/Screenshot_11.png)

## Cơ chế chuyển mạch Ethernet Switch

Chức năng chính của Switch là chuyển mạch: Quá trình nhận Frame, đẩy Frame qua port khác.

Dựa vào bảng chuyển mạch MAC table.

<iframe width="1280" height="720" src="https://www.youtube.com/embed/K8PCqhgLywk?list=PLhchcQ1p5Tc9_LOTMsjK_Mk2xZZR1VChu" title="Bài18: Cơ chế chuyển mạch Ethernet Switch" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Các kiểu truyền thông trên hệ thống mạng LAN

![](/images/CCNAPost/Screenshot_12.png)

## Cơ chế hoạt động của giao thức ARP phân giải địa chỉ IP thành địa chỉ MAC

Máy tính sử dụng ARP phân giải địa chỉ IP đích thành địa chỉ MAC tương ứng

Ví dụ, khi truyền dữ liệu từ PcA sang PcB, A không thể biết được MAC của B, nhưng từ địa chỉ IP của B, A có thể phân giải ra địa chỉ MAC tương ứng.

Khi này A sẽ soạn thảo bản tin ARP Request với MAC nguồn A và MAC đích là MAC POSTCARD, nó sẽ hỏi thông tin trong mạng là ai mang địa chỉ IP này, thì trả lại MAC cho A.

## Phân tích quá trình trao đổi dữ liệu giữa các phân vùng mạng LAN

Nếu cấu trúc Package có ý nghĩa trên toàn cầu, thì cấu trúc LAN chỉ có ý nghĩa trên từng phân vùng mạng.

![](/images/CCNAPost/Screenshot_13.png)

Nếu PcA muốn gửi gói tin tới B, PC A phải gửi gói tin tới Switch 1.
Đối với địa chỉ MAC R, gói tin sẽ đẩy qua port F0/4.
Router R1 đọc tiếp IP, muốn đẩy IP 20.0.0.0/24, phải đẩy qua port F0/2.
Trước khi gói tin gửi đi, nó xóa thông tin MAC nguồn MAC đích cũ, thêm MAC nguồn đích mới.

## Tìm hiểu cấu trúc địa chỉ MAC

Cấu trúc mạng LAN: 
![](/images/CCNAPost/Screenshot_14.png)

6 số HEXA đầu tiên trong địa chỉ MAC có thể tìm được ra nhà mạng sản xuất ra Card mạng đó thông qua trang web: aruljohn

## Công nghệ Ethernet LAN: Broadcast Domain

Bất kì thiết bị nào gửi Broadcast, tất cả các thiết bị đều nhận được lưu lượng Broadcast

Nếu trong cùng Broadcast Domain, mà 2 lớp mạng khác nhau. Có nguy cơ các thiết bị không thể giao tiếp được với nhau.

## Haft Duplex và Full Duplex trên Ethernet LAN

![](/images/CCNAPost/Screenshot_15.png)

Switch sau khi nhận được gói tin, sẽ phân tích địa chỉ MAC và gửi gói tin tới máy nhận

Hub xử lý tín hiệu 0101 trên môi trường truyền, khuếch đại tín hiệu trên tất cả các PORT => Giảm Perfomance, bảo mật.

![](/images/CCNAPost/Screenshot_16.png)

Đối với các thiết bị sử dụng Switch kết nối, chúng có thể truyền thông ở chế độ Full Duplex, tức là có thể đồng thời vừa truyền vừa nhận.

Đối với các thiết bị sử dụng Hub kết nối, chúng chỉ có thể truyền thông ở chế độ Half Duplex, chỉ có thể truyền dữ liệu, thiết bị này truyền thì thiết bị khác không thể truyền được nữa.

## Collision domain

![](/images/CCNAPost/Screenshot_17.png)

Khi 2 thiết bị truyền dữ liệu đồng thời thông qua Hub, sẽ gây ra hiện tượng Collision

Để tránh Collision domain, nên sử dụng switch, hoặc PC sẽ lắng nghe môi trường, sử dụng cơ chế Timer

## Xác định số lượng Collision Domain và Broadcast Domain trên mạng LAN

![](/images/CCNAPost/Screenshot_18.png)

Ở hình trên, chúng ta có 3 port của switch, tương ứng với 3 Collision Domain

![](/images/CCNAPost/Screenshot_19.png)

## Cấu trúc địa chỉ IPv4

IPv4 có 32 bit nhị phân, để dễ nhớ người ta thường đổi thành hệ cơ số 10. Người ta sẽ chia nhỏ địa chỉ IP thành 4 phần, đổi cơ số từng phần và đặt dấu chấm ở giữa.

## Các lớp của địa chỉ IPv4

![](/images/CCNAPost/Screenshot_20.png)

## Đổi từ Prefix Length thành Subnet Mask

Nếu Prefix-Length bằng 24, chúng ta viết 24 số 1, còn lại là 0.

Đổi thành thập phân mỗi 8 bit

![](/images/CCNAPost/Screenshot_21.png)




