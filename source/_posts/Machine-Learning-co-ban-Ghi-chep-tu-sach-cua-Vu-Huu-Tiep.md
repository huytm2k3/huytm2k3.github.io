---
title: Machine Learning cơ bản - Ghi chép từ sách của Vũ Hữu Tiệp
date: 2023-01-31 14:18:34
tags:
---

# Ôn tập Đại số tuyến tính

## Chuyển vị và Hermitian

![](/images/MLPost/Screenshot_1.png)

Nếu 2 ma trận sau khi chuyển vị vẫn giống nhau, vậy ma trận đó là ma trận <b>đối xứng</b>

Nếu ma trận hay vector có các phần tử là số phức, ta sử dụng phép toán chuyển <i>Chuyển vị liên hợp</i>

![](/images/MLPost/Screenshot_2.png)

Nếu ma trận sau khi chuyển vị liên hợp vẫn không thay đổi, ta nói ma trận đó là <i>Hermitian</i>

## Nhân 2 ma trận

![](/images/MLPost/Screenshot_3.png)

Các tính chất của phép nhân ma trận:

1. Không có tính giao hoán.
2. Có tính kết hợp: ABC = (AB)C = A(BC)
3. Có tính phân phối đối với phép cộng: A(B + C) = AB + AC
4. Chuyển vị của một tích bằng tích các chuyển vị theo thứ tự ngược lại. Điều tương tự xảy ra với Hermitian của một tích:

![](/images/MLPost/Screenshot_4.png)

Tích vô hướng của 2 vector x, y:

![](/images/MLPost/Screenshot_5.png)

<b>Note: Nếu tích vô hướng của 2 vector khác 0 bằng 0, 2 vector trực giao</b>

![](/images/MLPost/Screenshot_7.png)

Ví dụ:

![](/images/MLPost/Screenshot_6.png)

<i>Tích Hadamard</i> hay là phép nhân 2 ma trận cùng kích thước:

![](/images/MLPost/Screenshot_8.png)

## Ma trận đơn vị và ma trận nghịch đảo

### Ma trận đơn vị

Ma trận đơn vị bậc 3 và 4:

![](/images/MLPost/Screenshot_9.png)

<b>Note: </b>
![](/images/MLPost/Screenshot_10.png)

### Ma trận nghịch đảo

Phương pháp tìm ma trận nghịch đảo với biến đổi sơ cấp:

![](/images/MLPost/Screenshot_11.png)

Nếu ma trận có ma trận nghịch đảo, ta gọi đó là <i>ma trận khả nghịch</i>

<i>Ma trận nghịch đảo</i> thường được sử dụng để giải hệ phương trình tuyến tính: <b>Ax = b</b> <=> <b>x = A^-1.b</b>

## Một vài ma trận đặc biệt khác

### Ma trận đường chéo

Là ma trận mà các thành phần khác 0 chỉ nằm trên đường chéo chính

![](/images/MLPost/Screenshot_12.png)

Nếu ma trận đường chéo vuông, ta có thể kí hiệu:  diag(a11, a22, . . . , amm)

### Ma trận tam giác

<b>Ma trận tam giác</b> là các phần tử khác 0 đều nằm dưới đường chéo chính

![](/images/MLPost/Screenshot_13.png)

Các hệ phương trình tuyến tính với ma trận hệ số ở dạng tam giác có thể giải mà không cần tính ma trận nghịch đảo:

![](/images/MLPost/Screenshot_14.png)

## Định thức

