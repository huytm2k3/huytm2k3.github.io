---
title: File nhị phân trong C (Binary File)
date: 2022-04-24 16:52:50
tags: [C,file,binary-file]
---
## Mở đầu

Bài viết này dựa trên 3 tiếng tìm hiểu về đọc/ghi file nhị phân trong C. Sẽ cố gắng chia sẻ những thứ cơ bản mình biết về nó, hi vọng phần nào đó sẽ giúp đỡ các bạn trong quá trình học.

Mọi thắc mắc xin liên hệ tới:
- Facebook: https://www.facebook.com/profile.php?id=100072417355186 (Tạ Minh Huy)
- Zalo: 0522566897
- Email: Huyat180522@gmail.com

## Khái niệm

Source: https://www.techtarget.com/whatis/definition/binary-file#:~:text=A%20binary%20file%20is%20a,certain%20place%20within%20the%20file.

Dù Google có rất nhiều nhưng mình xin tóm tắt lại:
Tệp nhị phân là một tệp mà nội dung của nó phải được chương trình hoặc bộ xử lý phần cứng hiểu trước chính xác cách nó được định dạng. Có nghĩa là, tệp không ở bất kỳ định dạng có thể nhận dạng bên ngoài nào để bất kỳ chương trình nào muốn tìm kiếm dữ liệu nhất định tại một vị trí nhất định trong tệp.

## Cách dùng


### Khai báo file
Trước tiên, chúng ta cần khai báo một con trỏ kiểu file. Việc khai báo này là cần thiết để có sự kết nối giữa chương trình và tập tin cần thao tác.

```C
FILE *f;
```

### Thao tác mở file

Cấu trúc hàm fopen(): 
```
fopen(<filename>,<mode>)
// Example:

fopen("myFile.txt","wb") // wb: write binary (Ghi kiểu nhị phân)
// wb cho phép bạn mở và ghi vào file theo kiểu nhị phân.
fopen("myFile.txt,"rb") // rb: read binary (Đọc file theo kiểu nhị phân)
// rb chỉ cho phép bạn đọc mà không được ghi (Nhị phân).
```

### Thao tác ghi file

Hàm fwrite():
```C
fwrite(address_data,size_data,numbers_data,pointer_to_file);
```
Example:
```C
#include <stdio.h>
#include <stdlib.h>
 
struct threeNum
{
   int n1, n2, n3;
};
int main()
{
   int n;
   struct threeNum num;
   FILE *fptr;
 
   if ((fptr = fopen("C:\\program.bin","wb")) == NULL){
       printf("Error! opening file");
 
       // Program exits if the file pointer returns NULL.
       exit(1);
   }
 
   for(n = 1; n < 5; ++n)
   {
      num.n1 = n;
      num.n2 = 5*n;
      num.n3 = 5*n + 1;
      fwrite(&num, sizeof(struct threeNum), 1, fptr); 
   }
   fclose(fptr); 
  
   return 0;
}
```
### Thao tác đọc file

Hàm fread():

```C
fread(address_data,size_data,numbers_data,pointer_to_file);
```

Example:
```C
#include <stdio.h>
#include <stdlib.h>
 
struct threeNum
{
   int n1, n2, n3;
};
 
int main()
{
   int n;
   struct threeNum num;
   FILE *fptr;
 
   if ((fptr = fopen("C:\\program.bin","rb")) == NULL){
       printf("Error! opening file");
 
       // Program exits if the file pointer returns NULL.
       exit(1);
   }
 
   for(n = 1; n < 5; ++n)
   {
      fread(&num, sizeof(struct threeNum), 1, fptr); 
      printf("n1: %d\tn2: %d\tn3: %d", num.n1, num.n2, num.n3);
   }
   fclose(fptr); 
  
   return 0;
}
```

Bài tập mẫu của phần này là: Nhập vào danh sách sinh viên, ghi vào file theo kiểu nhị phân.

Full source code: http://codepad.org/aZlVtgsd

