---
title: SQL - Truy vấn cơ bản
date: 2022-11-22 06:48:44
tags:
---

- Khóa chính để định danh cho bảng, duy nhất.
- Mỗi bảng chỉ có một khóa chính.

Dưới đây sử dụng truy vấn SQL Server, với MySQL hay PostgreSQL syntax chỉ khác một chút.

Tạo 1 database:

```sql
CREATE DATABASE QUANLYSINHVIEN
```

Xóa 1 database:

```sql
DROP DATABASE QUANLYSINHVIEN
```

Tạo 1 bảng:

```sql
CREATE TABLE SinhVien(
    MSSV char(5) NOT NULL, -- Character có 5 kí tự
    HOTEN nvarchar(50) -- Character có unicode 50 kí tự
    --- ...
)
```
Xóa 1 bảng dùng drop

Các kiểu dữ liệu trong SQL: https://viblo.asia/p/sql-data-types-L4x5xGerlBM

Thêm khóa chính vào bảng đã tạo:

```SQL
ALTER TABLE SinhVien
ADD CONSTRAINT PK_SINHVIEN -- Tên constraint, dòng đặt tên này có thể bỏ đi - khi đó hệ thống tự đặt tên
PRIMARY KEY (MSSV)
```

Muốn thêm khóa chính thì trường đó phải là NOT NULL

Tạo khóa chính từ lúc tạo bảng:

```sql
CREATE TABLE MonHoc(
    MaMH CHAR(5),
    TenHM NVARCHAR(20),
    CONSTRAINT PK_MONHOC
    PRIMARY KEY (MaMH)
)
```

Sửa một cột trong bảng đã tạo:

```sql
ALTER TABLE MonHoc
ALTER COLUMN TenMH NVARCHAR(30)
```

Xóa ràng buộc:

```sql
ALTER TABLE <tenbang>
DROP CONSTRAINT <tenrangbuoc>
```
Thêm cột:

```sql
ALTER TABLE <tenbang>
ADD <tencot> <kieudulieu>
```

Tạo khóa ngoại cho bảng GiaoVien nối tới khóa chính MaKhoa:

Thêm 1 cột cho GiaoVien

```sql

-- Thêm 1 cột cho GiaoVIen

ALTER TABLE GiaoVien
ADD MAKHOA CHAR(5)

-- Tạo table Khoa

CREATE TABLE Khoa(
    MaKhoa CHAR(5)
    TenKhoa NVARCHAR(50),
    PRIMARY KEY(MaKhoa)
)

-- Tạo khóa ngoại

ALTER TABLE GiaoVien
ADD CONSTRAINT FK_GV_KHOA
FOREIGN KEY (MaKhoa)
REFERENCES Khoa (MaKhoa)

```

Nhập dữ liệu vào 1 bảng:

``` sql
INSERT INTO SinhVien (MSSV, HOTEN) VALUES ('001', 'Ta Minh Huy')
```

![](/images/SQLPost/Screenshot_1.png)

Hiển thị dữ liệu 1 bảng:

```sql
SELECT <cot>
FROM <tenbang>
WHERE <dieukien>
```

Sử dụng điều kiện với Date

```sql
SELECT * FROM SinhVien
WHERE MONTH(NGAYSINH) = 10 -- Lấy những sinh viên sinh tháng 10
```

