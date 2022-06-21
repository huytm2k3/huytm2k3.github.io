---
title: Lập trình Android với Kotlin Basic
date: 2022-05-09 15:43:35
tags: [kotlin, android]
categories: [Front-end]
---
## Mở đầu

Kotlin là ngôn ngữ lập trình được phát triển bởi JetBrains. Nó xuất hiện lần đầu năm 2011 khi JetBrains công bố dự án của họ mạng tên "Kotlin". Đây là một ngôn ngữ mã nguồn mở

Về cơ bản, cũng như Java, C hay C++ , Kotlin cũng là "ngôn ngữ lập trình kiểu tĩnh". Nghĩa là các biến không cần phải định nghĩa trươc khi sử dụng. Kiểu tĩnh thực hiện việc kê khai nghiêm ngặt hoặc khởi tạo các biến trước khi chúng được sử dụng

Mọi thắc mắc xin liên hệ tới:
- Facebook: https://www.facebook.com/profile.php?id=100072417355186 (Tạ Minh Huy)
- Zalo: 0522566897
- Email: Huyat180522@gmail.com

Hiện tại thì mình vẫn đang học về ngôn ngữ này, chắc chắn sẽ có nhiều sai sót và thiếu sót, mình sẽ cố gắng hoàn thiện POST này một cách đầy đủ và dễ hiểu nhất có thể! <3

## Variable

Cấu trúc khai báo một biến:
```Kotlin
var <ten bien> : <kieu du lieu> = <gia tri>
val <ten hang> : <kieu du lieu> = <gia tri>
```
Khởi tạo biến với var thì có thể thay đổi giá trị, còn với val thì không
```Kotlin
var str1 : String = "Hello world"
str1 = "Hello world was changed"
val str2 : String = "Hello boss"
str2 = "FU" // Báo lỗi
```

## Null safety
Trong Kotlin, có một cái lỗi rất khó chịu mà khi compiler IDE không báo lỗi, đó là Null pointer.
Vì vậy chúng ta sẽ tìm hiểu về Null safety.

Với một biến (có kiểu dữ liệu và giá trị) không thể bị gán lại bằng Null: 
```Kotlin
var name : String = "Ta Minh Huy"
name = null // Báo lỗi
```
Nếu muốn thực hiện điều đó, sau kiểu dữ liệu hãy thêm dấu "?":
```Kotlin
var name : String? = "Ta Minh Huy"
name = null // Không lỗi
```
Ép kiểu: Dùng hàm toInt(), toString(), ...
Example:
```Kotlin
    var strToInt : String = "3";
    Log.d("strToIntLog", (strToInt+2).toString()) // Output: 5
```
## If else
Chắc hẳn là nếu đã học tới tận Kotlin thì trước đó phải nắm vững kiến thức lập trình của ít nhất một trong các ngôn ngữ cơ bản như Pascal, C/C++ hoặc python rồi.
Thì phần If else này tôi sẽ không nói quá nhiều vì nó khá giống với những ngôn ngữ khác.

```Kotlin
var a : Int = 10
var b : Int = 15

if(a>b){
    Log.d("compareLog", "Giá trị lớn nhất là: " + a)
}else if(a<b){
    Log.d("compareLog", "Giá trị lớn nhất là: " + b)
}else{
    Log.d("compareLog", "a = b")
}

## Bài viết đang hoàn thiện..
```