---
title: Tìm hiểu về android
date: 2022-03-30 16:00:44
tags:
---

## 1. Các phần cơ bản trong 1 project android.

- App/java: Chứa các file java của từng layout (giống js trong lt web)
- Res/drawable: Chứa ảnh
- Res/layout: chứa layout(giao diện, giống html, css trong lập trình web
- Res/mipmap: chứa icon, có thể là icon của app
- Res/value: chứa các chuỗi, các định dạng màu để gọi cho dễ

## 2. Các layout dùng trong android.

- LinearLayout: Phần tử sắp xếp không trùng nhau:
    - Orientation (Sắp xếp ngang hoặc dọc):
        - Horizontal (Ngang)
        - Vertical (Dọc)
- RelativeLayout: Phần tử sắp xếp trùng nhau



## 3. Các View cơ bản hay dùng trong android layout.

- TextView: Văn bản
- EditText: TextBox
- Button: Nút
- RadioButton: Nút dùng để lấy 1 lựa chọn duy nhất
- CheckBox: Chọn nhiều lựa chọn
- Spinner: Danh sách lựa chọn
- DatePicker: Chọn ngày
- TimePicker: Chọn giờ
- ScrollView: Tạo thanh cuộn
- ListView: Danh sách
### 1. TextView
### 2. EditText
### 3. Button
### 4. RadioButton
    isChecked() trả về True False (Code Java)
### 5. CheckBox
    isChecked() trả về True False (Code Java)
![](/images/AndroidPost/a1.png)
### 6. Spinner
![](/images/AndroidPost/a2.png)
##### Cách tạo danh sách trong Spinner:
    B1. Tạo List chứa danh sách:
    ![](/images/AndroidPost/a3.png)
    B2. Tạo ArrayAdapter, cho List vào ArrayAdapter:
    ![](/images/AndroidPost/a4.png)
    B3. Cho adapter vào Spinner:
    ![](/images/AndroidPost/a5.png)
##### Sự kiện trong Spinner:
    ![](/images/AndroidPost/a6.png)
    onItemSelected: Khi item được chọn
    onNothingSelected: Khi không item nào được chọn
### 7. DatePicker
    ![](/images/AndroidPost/a7.png)
    Hàm init khởi tạo ngày ban đầu của DatePicker hiển thị
    ![](/images/AndroidPost/a8.png)
    Lấy ngày hiện tại của thiết bị:
    ![](/images/AndroidPost/a9.png)
    Hiển thị ngày vừa chọn:
    ![](/images/AndroidPost/a10.png)
### 8. TimePicker
Hiển thị giờ vừa chọn:
![](/images/AndroidPost/a11.png)
### 9. ScrollView
## 3. Dialog và AlertDialog
### a. Dialog
Tạo 1 dialog layout trong thư mục res/layout:
![](/images/AndroidPost/a12.png)
setContentView dùng để xác định dialog nào trong layout được hiện lên
Hàm .show() dùng để hiển thị dialog
Lấy view trong dialog dùng cần phải dialog.findViewById
Hàm .dismiss() dùng để đóng dialog
### b. AlertDialog
![](/images/AndroidPost/a13.png)
Click ra ngoài AlertDialog sẽ thoát AlertDialog:
![](/images/AndroidPost/a14.png)
Nếu để false thì ngược lại (Quan trọng)
## 4. ListView
Khởi tạo ListView ở Layout:
![](/images/AndroidPost/a15.png)
Thao tác với ListView:
![](/images/AndroidPost/a16.png)
 
ListView hiển thị theo cách thức simple_list_item_1 chỉ là cách hiển thị đơn giản, có thể custom ListView ở mục sau:
![](/images/AndroidPost/a17.png)
 
Sự kiện khi click vào 1 item trong ListView
![](/images/AndroidPost/a18.png)
![](/images/AndroidPost/a19.png)
![](/images/AndroidPost/a20.png)
## 5. Custom ListView
![](/images/AndroidPost/a21.png)
![](/images/AndroidPost/a22.png)
![](/images/AndroidPost/a23.png)
Dùng tổ hợp phím Alt + ins.