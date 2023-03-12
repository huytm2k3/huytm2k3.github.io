---
title: Thuật toán trong An toàn thông tin - Part 1
date: 2023-03-12 11:12:47
tags:
---

Trước khi bắt đầu nội dung thì chúng ta cần tiếp thu một chút hiểu biết về ngành An toàn thông tin và tầm quan trọng của nó.

## An toàn thông tin là gì?

<b>An toàn thông tin</b> được hiểu là một hành động nhằm phòng ngừa, ngăn chặn hoặc ngăn cản sự truy cập, sử dụng, chia sẻ thông tin, tiết lộ, phát tán, phá hủy hoặc ghi lại những thông tin khi chưa được sự cho phép của chủ sở hữu.
Nguồn: Wikipedia

Thầy dạy tôi môn này có nói một câu: "Nếu Công nghệ thông tin là học về vẽ chiếc bàn 2D, thì An toàn thông tin là căn phòng học 3D" hay "90% kĩ sư An toàn thông tin ra trường làm về Công nghệ thông tin".

Bản thân tôi thấy, ngành Công nghệ thông tin cực kì rộng lớn, vốn dĩ An toàn thông tin chỉ là 1 nhánh nhỏ rất nhỏ trong lĩnh vực Công nghệ thông tin, nhưng một số bạn trẻ ngày nay có xu hướng nhầm với việc học IT chính là "Viết Code". Cái "Viết Code" đó có lẽ nên nói về ngành Kĩ thuật phần mềm nhiều hơn.

Mặc dù là một nhánh nhỏ trong Công nghệ thông tin, nhưng An toàn thông tin lại đóng vai trò to lớn cho toàn ngành.

## Thuật toán trong An toàn thông tin.

### Tính toán trên số nguyên lớn

#### Thuật toán cộng chính xác bội - Multiprecision addition

VD: Cho a = (0, 11, 173, 248); b = (0, 1, 226, 64), với w = 8, t = 4. Tìm c = a + b mod pow(2, Wt)
```py
a = [0, 11, 173, 248]
b = [0, 1, 226, 64]
W = 8
t = 4

def solve(a, b, W, t):
	a.reverse()
	b.reverse()
	c = []
	epsilon = 0
	e = pow(2, 8)
	for i in range(t):
		s = a[i] + b[i] + epsilon
		x = s%e
		if(s > e): epsilon = 1
		else: epsilon = 0 
		c.append(x)
	return [epsilon, c[::-1]]
	
if __name__ == '__main__':
	print(solve(a, b, W, t))
```

#### Thuật toán trừ chính xác bội - Multiprecision subtraction

VD: Cho a = (0, 11, 173, 248); b = (0, 1, 226, 64), với w = 8, t = 4. Tìm c = a - b mod pow(2, Wt)
```py
a = [0, 11, 173, 248]
b = [0, 1, 226, 64]
W = 8
t = 4

def solve(a, b, W, t):
	a.reverse()
	b.reverse()
	c = []
	epsilon = 0
	e = pow(2, 8)
	for i in range(t):
		d = a[i] - b[i] - epsilon
		if(d < 0): 
			d += e
			epsilon = 1
		else: epsilon = 0
		x = d%e
		c.append(x)
	return epsilon, c[::-1]

if __name__ == '__main__':
	print(solve(a, b, W, t))
```

#### Thuật toán cộng trên trường hữu hạn Fp

Cho p = 2.147.483.647, W = 8; a = (0, 11, 173, 248); b = (0, 1, 226, 64). 3 Tìm c = a + b mod p

```py
import math, re

p = 2147483647
a = [157, 0, 173, 23]
b = [169, 1, 0, 64]
W = 8
m = round(math.log2(p))
t = round(m/W)

def int_to_dec(n):
	n = bin(n)[2:].zfill(8*t)
	b = re.findall('\d{8}', n)
	c = ['0b' + i for i in b]
	return [int(i, 2) for i in c]

def dec_to_int(n):
	n = ''.join([bin(i)[2:].zfill(8) for i in n])
	return int(n, 2)


def multiprecision_addition(a, b, W, t):
	a.reverse()
	b.reverse()
	c = []
	epsilon = 0
	e = pow(2, 8)
	for i in range(t):
		s = a[i] + b[i] + epsilon
		x = s%e
		if(s > e): epsilon = 1
		else: epsilon = 0 
		c.append(x)
	return [epsilon, c[::-1]]

def multiprecision_subtraction(a, b, W, t):
	a.reverse()
	b.reverse()
	c = []
	epsilon = 0
	e = pow(2, 8)
	for i in range(t):
		d = a[i] - b[i] - epsilon
		if(d < 0): 
			d += e
			epsilon = 1
		else: epsilon = 0
		x = d%e
		c.append(x)
	return epsilon, c[::-1]

if __name__ == '__main__':
	[epsilon, c] = multiprecision_addition(a, b, W, t)
	p = int_to_dec(p)
	if epsilon == 1:
		d = multiprecision_subtraction(c, p, W, t)
	elif epsilon == 0:
		d = multiprecision_subtraction(p, c, W, t)
	print(d)	

```

#### Thuật toán trừ trên trường hữu hạn Fp

Cho p = 2.147.483.647, W = 8; a = (0, 11, 173, 248); b = (0, 1, 226, 64). 3 Tìm c = a - b mod p

```py
import math, re

p = 2147483647
a = [0, 11, 173, 248]
b = [0, 1, 226, 64]
W = 8
m = round(math.log2(p))
t = round(m/W)

def int_to_dec(n):
	n = bin(n)[2:].zfill(8*t)
	b = re.findall('\d{8}', n)
	c = ['0b' + i for i in b]
	return [int(i, 2) for i in c]

def dec_to_int(n):
	n = ''.join([bin(i)[2:].zfill(8) for i in n])
	return int(n, 2)

def multiprecision_addition(a, b, W, t):
	a.reverse()
	b.reverse()
	c = []
	epsilon = 0
	e = pow(2, 8)
	for i in range(t):
		s = a[i] + b[i] + epsilon
		x = s%e
		if(s > e): epsilon = 1
		else: epsilon = 0 
		c.append(x)
	return [epsilon, c[::-1]]

def multiprecision_subtraction(a, b, W, t):
	a.reverse()
	b.reverse()
	c = []
	epsilon = 0
	e = pow(2, 8)
	for i in range(t):
		d = a[i] - b[i] - epsilon
		if(d < 0): 
			d += e
			epsilon = 1
		else: epsilon = 0
		x = d%e
		c.append(x)
	return epsilon, c[::-1]

if __name__ == '__main__':
	[epsilon, c] = multiprecision_subtraction(a, b, W, t)
	p = int_to_dec(p)
	if epsilon == 1:
		d = multiprecision_addition(c, p, W, t)
	elif epsilon == 0:
		d = c
	print(d)	

```
### Số nguyên tố

### Đối sánh mẫu trên chuỗi



