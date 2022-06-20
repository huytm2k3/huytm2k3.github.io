---
title: Tìm hiểu về Java OOP (Hướng đối tượng)
date: 2022-03-30 16:36:01
tags: [java, javaOOP]
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
<!--more-->
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
## Interface: Là một kiểu trừu tượng tham chiếu trong java, nó tương tự như class nhưng có những điểm đặc biệt.
![](/images/JavaPost/a45.png)
### Interface attributes
![](/images/JavaPost/a46.png)
### Interface methods
![](/images/JavaPost/a47.png)
### Interface labs
Tạo Interface: Chuột phải vào Package/New/Interface:
![](/images/JavaPost/a48.png)
![](/images/JavaPost/a49.png)
![](/images/JavaPost/a50.png)
![](/images/JavaPost/a51.png)
## Abstract Class
![](/images/JavaPost/a52.png)
![](/images/JavaPost/a53.png)
![](/images/JavaPost/a54.png)
![](/images/JavaPost/a55.png)
## Inheritance
Cách để sử dụng lại tài nguyên của class
![](/images/JavaPost/a56.png)
## Inheritance Labs
Một Class thừa kế 1 Class, 1 class thừa kế 1 interface:
![](/images/JavaPost/a57.png)
- 1 Class chỉ có thể thừa kế 1 class
- 1 class có thể thừa kế đa interface:
![](/images/JavaPost/a58.png)
![](/images/JavaPost/a59.png)
Nếu class Developer thừa kế của class Employee:
![](/images/JavaPost/a60.png)
Thì class Manager có thể dùng như này:
![](/images/JavaPost/a61.png)
## Abstraction
![](/images/JavaPost/a62.png)
## Abstraciton Labs
![](/images/JavaPost/a63.png)
![](/images/JavaPost/a64.png)
2 class Student và Employee cùng dùng hàm move() của Person nhưng theo 2 cách khác nhau.
## Encapsulation (Tăng tính che giấu bảo mật của object)
## Encapsulation Labs
Ở những mục trước, chúng ta đã khai báo biến name ở Employee với private
![](/images/JavaPost/a65.png)
Nên chỉ có thể dùng getters and setters.
## Polymorphism (Đa hình)
Một name – nhiều form.
![](/images/JavaPost/a66.png)
## Java OOP Recap
![](/images/JavaPost/a67.png)
- Về mặt cơ bản thì đều có đặc điểm là che giấu
- Với Abstraction: Che giấu chi tiết cách để tạo ra phương thức.
- Encapsulation: Che giấu về mặt dữ liệu.
![](/images/JavaPost/a68.png)
## Java Identifiers
## Java Keywords
![](/images/JavaPost/a69.png)
## Java Naming Convention
![](/images/JavaPost/a70.png)
## Java Naming Convention Labs
- Upper case: MYPACKAGE
- Lower case: mypackage
- Camel case: MyPackage ( Lạc đà )
- Mixed case – Lower camel case: myPackage
![](/images/JavaPost/a71.png)
![](/images/JavaPost/a72.png)
## Global Variable Labs
## Local Variable Labs
![](/images/JavaPost/a73.png)
## Primitive Data Types (Dữ liệu nguyên thủy):
![](/images/JavaPost/a74.png)
## Primitive Data Types Labs
![](/images/JavaPost/a75.png)
## Autoboxing vs Unboxing
## Variable Initialization
## Variable Initialization Labs
![](/images/JavaPost/a76.png)
Final variable phải được đặt giá trị, final variable không được thay đổi giá trị.
![](/images/JavaPost/a77.png)
## Garbage Collection (GC)
Loại bỏ những unreferenced object khỏi bộ nhớ.
![](/images/JavaPost/a78.png)
![](/images/JavaPost/a79.png)
![](/images/JavaPost/a80.png)
## Garbage Collection Labs
![](/images/JavaPost/a81.png)
![](/images/JavaPost/a82.png)
![](/images/JavaPost/a83.png)
## Variable Scope (Phạm vi của biến):
## Java Heap and Stack:
- Các biến và Object được lưu trữ ở đâu liên quan đến Java Heap and Stack?
- Bộ nhớ của Heap để lưu trữ những Object.
- Java Stack lưu trữ những phương thức, Local variables và reference variables.
## Arithmetic Operatiors (Toán tử số học)
![](/images/JavaPost/a84.png)
## Assignment Operators
![](/images/JavaPost/a85.png)
## Relational Operators
![](/images/JavaPost/a86.png)
## Instanceof
Kiểm tra các Object để xem nó có phải 1 đối tượng, 1 đại diện hay 1 class cụ thể không.
## Instanceof Labs
![](/images/JavaPost/a87.png)
## Logical Operators
![](/images/JavaPost/a88.png)
![](/images/JavaPost/a89.png)
## Logical Operators Labs
![](/images/JavaPost/a90.png)
## Declare Arrays
![](/images/JavaPost/a91.png)
## Multi-dimension Array
![](/images/JavaPost/a92.png)
## Access Array Elements
![](/images/JavaPost/a93.png)
## Array Labs
![](/images/JavaPost/a94.png)
## Array Initialization
![](/images/JavaPost/a95.png)