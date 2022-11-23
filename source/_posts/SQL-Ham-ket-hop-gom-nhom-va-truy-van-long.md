---
title: SQL - Hàm kết hợp, gom nhóm và truy vấn lồng
date: 2022-11-22 13:53:17
tags:
---

## Inner Join

Kết hợp 2 bảng, lấy ra trường thỏa mãn điều kiện.

```sql
-- Inner join kiểu cũ

SELECT * FROM GIAOVIEN, BOMON
WHERE BOMON.MABM = GIAOVIEN.MABM

-- Inner join kiểu mới

SELECT * 
FROM GIAOVIEN INNER JOIN BOMON
ON BOMON.MABM = GIAOVIEN.MABM
```

## Full Out Join

Phần này khó giải thích quá ạ =))

```sql
SELECT * FROM GIAOVIEN FULL OUTER JOIN BOMON
ON BOMON.MABM = GIAOVIEN.MABM
```

## Left - Right Join



```sql
-- Left join

SELECT * FROM BOMON LEFT JOIN GIAOVIEN
ON BOMON.MABM = GIAOVIEN.MABM

-- Right join

SELECT * FROM BOMON RIGHT JOIN GIAOVIEN
ON BOMON.MABM = GIAOVIEN.MABM

```

Với LEFT JOIN, các row trong table BOMON sẽ đi tìm các row của table GIAOVIEN thỏa mãn điều kiện để ghép nối với chúng (điều kiện ở đây là ON BOMON.MABM = GIAOVIEN.MABM), với RIGHT JOIN thì ngược lại.

Một giáo viên, dạy một bộ môn thì chắc chắn kết quả sẽ không bao gồm null, vì chắc chắn tồn tại bộ môn đó, nên LEFT JOIN trong trường hợp này không bị NULL.

Một bộ môn, chưa chắc đã có giáo viên dạy, nên trường hợp này có thể bị null

## Union

Gộp 2 bảng lại với nhau, lấy ra các row duy nhất chứ không bị lặp lại

## SELECT INTO

Sao chép dữ liệu ra một bảng chưa tạo

```sql

-- Lấy hết dữ liệu của bảng GIAOVIEN đưa vào bảng mới tên là TableA

SELECT * INTO TableA
FROM GIAOVIEN 

-- Tạo ra bảng TableB mới có 1 trường HoTen, sao chép dữ liệu từ bảng GIAOVIEN

SELECT HoTen INTO TableB
FROM GiAOVIEN

-- Tạo ra bảng TableC mới có 1 trường HoTen, lấy dữ liệu từ bảng GIAOVIEN với những giáo viên có lương > 2000

SELECT HoTen INTO TableB
FROM GIAOVIEN
WHERE LUONG > 2000

```

## INSERT INTO SELECT

```sql

-- Tạo ra một bảng CLoneGV có các trường giống GIAOVIEN nhưng không có dữ liệu

SELECT * IN CLoneGV
FROM GIAOVIEN
WHERE 1=0

-- Sao chép dữ liệu 

INSERT INTO CloneGV
SELECT * FROM GIAOVIEN

```

## Truy vấn lồng

Nếu ta có 1 table như này:

![](/images/SQLAdvPost/Screenshot_1.png)

Để kiểm tra GV001 có nằm trong danh sách GVQLCM hay không, chúng ta dùng truy vấn lồng. Nếu GV 001 nằm trong danh sách GVQLCM, in ra thông tin GV 001

```sql
SELECT * FROM GIAOVIEN
WHERE MAGV = '001'
AND MAGV IN
(
    SELECT GVQLCM FROM GIAOVIEN
)
```

Truy vấn lồng trong form

```sql
SELECT * FROM
GIAOVIEN, (SELECT * FROM DETAI) AS DT
-- ...
```


