---
title: Con trỏ trong C/C++(Pointer)
date: 2022-04-23 16:18:57
tags: [C,C++,C/C++,pointer]
---

## Mở đầu

Bài viết này dựa trên 5 tiếng tìm hiểu về con trỏ (Pointer) của mình. Sẽ cố gắng chia sẻ những thứ cơ bản mà mình biết về nó, hi vọng phần nào đó sẽ giúp đỡ các bạn trong quá trình học.

Mọi thắc mắc xin liên hệ tới:
- Facebook: https://www.facebook.com/profile.php?id=100072417355186 (Tạ Minh Huy)
- Zalo: 0522566897
- Email: Huyat180522@gmail.com

## Khái niệm

Từ trước tới nay, con trỏ là thứ mà đa số các sinh viên IT năm nhất đau đầu. Vậy con trỏ (pointer) là gì?

Con trỏ thực tế cũng chỉ là một biến, có thể khai báo, khởi tạo và lưu trữ giá trị và có địa chỉ riêng của nó. Nhưng con trỏ không lưu trữ giá trị bình thường mà là lưu trữ địa chỉ.
Phần ví dụ tôi sẽ dùng ngôn ngữ C.

## Nội dung

Cấu trúc khai báo 1 biến con trỏ: 
```C
<Kieu du lieu> *<Ten bien>;
```
Example: 
```C
int *p; // Trỏ tới địa chỉ biến kiểu nguyên
float *p; // Trỏ tới địa chỉ biến kiểu thực
char *p; // Trỏ tới địa chỉ biến kiểu kí tự
void *p; // Có thể trỏ tới bất kì địa chỉ của kiểu dữ liệu nào
```

Vậy thì tác dụng của con trỏ là gì? Hãy xem thử con trỏ có quyền năng gì nhé.

Example:

```C
int a = 5;
int *p = &a; // Trỏ tới địa chỉ của biến a

printf("%d",p); // Output : Địa chỉ của biến a (Tương đương với in ra &a)
printf("%d",&p); // Output: Địa chỉ của biến p (Biến con trỏ)
printf("%d",*p); // Output: Giá trị của biến a (5)
// Vì con trỏ p trỏ tới địa chỉ của a, tức là p có thể làm thay đổi được giá trị của a
*p = 10;
printf("%d",a); // Output: 10 (Giá trị biến a đã được thay đổi)
```

Một tác dụng mà mình thấy khá hữu ích trong môn lập trình căn bản là dùng con trỏ trong hàm con (Tham chiếu).
Tham chiếu, tham trị là gì? Chúng khác nhau chỗ nào?

Ví dụ bằng một hàm quốc dân mà ai ai cũng dùng đi nhé.
```C
// Tham trị
void swap(int a,int b){
    int tmp;
    tmp = a;
    a = b;
    b = tmp;
}
int main(){
    int a = 5,b = 10;
    printf("Gia tri a va b truoc khi swap: a = %d, b = %d\n");
    swap(a,b);
    printf("Gia tri a va b sau khi swap: a = %d, b = %d\n");
}
// Output
// Gia tri a va b truoc khi swap: a = 5, b = 10
// Gia tri a va b sau khi swap: a = 5, b = 10
```
Biến a và b ở đây là biến cục bộ (Local Variable), hãy coi mỗi 1 hàm là một căn nhà, biến cục bộ chính là đồ vật trong nhà. Đồ nhà ai chỉ dùng được ở nhà đấy, khi truyền vào một tham trị sẽ được coi như là nhà "main" cho nhà "swap" mượn đồ. Nhưng chỉ là mượn để dùng mà không được thay đổi, phá hoại. Đây gọi là tham trị hay chính là nhà "swap" chỉ có thể sử dụng cái giá trị của a, b mà nhà "main" cho mượn mà không thể thay đổi giá trị của nó.

```C
// Tham chiếu
void swap(int *a,int *b){
    int tmp;
    tmp = a;
    a = b;
    b = tmp;
}
int main(){
    int a = 5,b = 10;
    printf("Gia tri a va b truoc khi swap: a = %d, b = %d\n");
    swap(&a,&b);
    printf("Gia tri a va b sau khi swap: a = %d, b = %d\n");
}
// Output
// Gia tri a va b truoc khi swap: a = 5, b = 10
// Gia tri a va b sau khi swap: a = 10, b = 5
```
Khi truyền vào tham chiếu, tức là nhà "main" cho phép nhà "swap" có thể thay đổi giá trị của biến.

Đó là cách nói dễ hiểu, thực chất là:
- Khi tham trị, hàm main chỉ truyền vào hàm swap là "giá trị" của a và b, nên dù có thay đổi cũng không ảnh hưởng đến giá trị của biến a, b ở hàm main.
- Khi tham chiếu, hàm main truyền vào chính là "địa chỉ" của biến a và b nên hàm swap có thể trực tiếp sửa đổi giá trị biến a, b ở hàm main.

Vì vậy, không phải ngẫu nhiên mà hàm scanf phải luôn truyền vào địa chỉ của một biến.
Bài viết này đang trong quá trình hoàn thiện thêm nội dung, Thank you for all <3 !
