---
title: Tìm hiểu về Java OOP (Hướng đối tượng)
date: 2022-03-30 16:36:01
tags:
---

## Java Feature
![](/images/JavaPost/a1.png)

## Chương trình Hello World
![](/images/JavaPost/a2.png)

## Compile chương trình để tạo ra file *.class

![](/images/JavaPost/a3.png)

## Run chương trình

![](/images/JavaPost/a4.png)

## IDE

Ở đây chúng ta sẽ dùng Eclipse

1. Tạo Project java : File/New/Project Java hoặc Alt + Shift + N. 
![](/images/JavaPost/a5.png)
2. Đặt tên project và chọn phiên bản java
![](/images/JavaPost/a6.png)
![](/images/JavaPost/a7.png)
3. Chạy chương trình với Eclipse:
![](/images/JavaPost/a8.png)
![](/images/JavaPost/a9.png)
### Eclipse WorkingSet
![](/images/JavaPost/a10.png)

### Code Template: /Window/Preferences
![](/images/JavaPost/a11.png)
![](/images/JavaPost/a12.png)
## Comment
Ctrl + "/": Comment theo dòng.
Ctrr + Shift + "/": Comment nhiều dòng.
## File *.jar

### Tạo file manifest.txt với Main-Class: HelloWorld
![](/images/JavaPost/a13.png)
### Đóng gói file jar
![](/images/JavaPost/a14.png)
![](/images/JavaPost/a15.png)
![](/images/JavaPost/a16.png)
### Chạy gói jar
![](/images/JavaPost/a17.png)
### Đóng gói jar trong IDE Eclipse
Chọn Project, File/Export:
![](/images/JavaPost/a18.png)
Location:
![](/images/JavaPost/a19.png)
## JavaClass
![](/images/JavaPost/a20.png)
Trong 1 file java có thể có nhiều class, nhưng chỉ có nhiều nhất 1 class khai báo là public, tên class public phải dùng đặt cho tên file java. Khi không có class nào public thì có thể đặt tên file java, hàm main phải nằm trong public class.
Tên public class không trùng với tên file:
![](/images/JavaPost/a21.png)
Tồn tại 2 public class:
![](/images/JavaPost/a22.png)
Hàm main không nằm trong public class:
![](/images/JavaPost/a23.png)
![](/images/JavaPost/a24.png)
## Package
Package được coi như 1 thư mục, 1 package có thể chứa nhiều package con khác hoặc chứa các file class, interface.
## Access modifiers
![](/images/JavaPost/a25.png)
![](/images/JavaPost/a26.png)
- Public: Cho phép truy cập tất cả mọi nơi
- Private: Chỉ cho phép truy cập trong chính class nó.
- Protected: Chỉ cho phép truy cập các lớp cùng package hoặc các lớp con ngoài package.
- Default: Chỉ cho phép các class cùng 1 package.

## Attributes (Class variables, Instance variables, DataMembers, Properties)
![](/images/JavaPost/a27.png)
![](/images/JavaPost/a28.png)
## Class Methods
![](/images/JavaPost/a29.png)
## Class Labs
![](/images/JavaPost/a30.png)
Vì class Employee là public, nên class Managerment có thể import.
Nếu khác package thì cần import, nếu cùng package thì không cần import.
Nhưng chúng ta không thể lấy biến name của Employee để Management sử dụng
![](/images/JavaPost/a31.png)
 
Vì biến name được khai báo dưới dạng private:
![](/images/JavaPost/a32.png)
Nếu biến name của Employee khai báo dưới dạng protected:
![](/images/JavaPost/a33.png)
thì chỉ những class có cùng Package có thể sử dụng biến đó, ở đây là class Manager.
## Constructors
- Là phương thức đặc biệt dùng để khởi tạo các object.
- Cùng tên với tên class (Bắt buộc).
- Không có giá trị trả về, kể cả void cũng không có.
- Mọi class đều có hàm khởi tạo.
- Các hàm khởi tạo có thể có tham số hoặc không.
- Sử dụng từ khóa new để khởi tạo object

## Constructors default
- Mặc định, mọi class đều có hàm khởi tạo không có tham số.
- Nếu chúng ta khai báo một hàm khởi tạo trong java thì ngay lập tức java sẽ loại bỏ với hàm khởi tạo mặc định này.

## Constructors Labs
![](/images/JavaPost/a34.png)
![](/images/JavaPost/a35.png)
Khi chạy Fresher sẽ chạy hàm Manager():
![](/images/JavaPost/a36.png)
Bây giờ hàm Manager() sẽ thay thế hàm khởi tạo mặc định.
Vì hàm khởi tạo không được truyền tham số, nếu muốn có hàm truyền tham số thì bắt buộc phải tạo hàm khởi tạo khác.
![](/images/JavaPost/a37.png)
![](/images/JavaPost/a38.png)
## Getters and Setters
Setter: Đặt giá trị
![](/images/JavaPost/a39.png)
Getter: Lấy giá trị
![](/images/JavaPost/a40.png)
## Getters and Setters Labs
Tạo tắt:
![](/images/JavaPost/a41.png)
![](/images/JavaPost/a42.png)
Hoặc ấn Alt + Shift + S, sau đó bấm R.
Khi đó, Class Manager sẽ lấy biến name theo:
![](/images/JavaPost/a43.png)
