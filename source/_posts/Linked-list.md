---
title: Danh sách liên kết (Linked List)
date: 2022-04-21 18:31:05
tags: [C,C++,C/C++,linked-list]
---

## Mở đầu

Bài viết này dựa trên 15 tiếng học Linked list của mình, sẽ chia sẻ tất cả những thứ cơ bản mà mình biết về nó.
Mọi thắc mắc xin liên hệ tới:
- Facebook: https://www.facebook.com/profile.php?id=100072417355186 (Tạ Minh Huy)
- Zalo: 0522566897
- Email: Huyat180522@gmail.com

### Khái niệm

Linked list hay còn gọi là danh sách liên kết, là một dãy các cấu trúc dữ liệu được kết nối với nhau thông qua các liên kết (link). Hiểu một cách đơn giản thì Danh sách liên kết là một cấu trúc dữ liệu bao gồm một nhóm các nút (node) tạo thành một chuỗi. Mỗi nút gồm dữ liệu ở nút đó và tham chiếu đến nút kế tiếp trong chuỗi.
Danh sách liên kết là cấu trúc dữ liệu được sử dụng phổ biến thứ hai sau mảng.

### Các loại danh sách liên kết

- Danh sách liên kết đơn (Simple linked list): Chỉ duyệt các phần tử theo chiều về trước.
- Danh sách liên kết đôi (Doubly linked list): Các phần tử có thể duyệt theo chiều về trước hoặc về sau.
- Danh sách liên kết vòng (Circular linked list): Phần tử cuối cùng chứa link của phần tử đầu tiên như là next và phần tử đầu tiên có link tới phần tử cuối cùng như là prev.

Ở bài viết này phần lớn mình sẽ chỉ nói về Danh sách liên kết đơn. ( 15 tiếng thì học được bao nhiêu đâu chứ =)) )

## Cấu trúc

Nói dễ hiểu hoặc có thể nói là theo ý hiểu của mình, danh sách liên kết được coi là 1 sợi dây xích, mà những node là những mắt xích, các mắt xích được nối với nhau bởi 1 con trỏ (từ giờ gọi là next).
Vậy mỗi node thì sẽ mang 2 thứ, 1 là dữ liệu của chính nó, 2 là next (để nối tới node tiếp theo).
Phần bài tập hướng dẫn này sẽ liên quan tới quản lý sinh viên (Quốc dân cmnr!)
Yêu cầu đặt ra:
- [ ] Có kiến thức nền tảng về C hoặc C++.
- [ ] Đã học về struct.
- [ ] Biết những thứ cơ bản về con trỏ.

### Khai báo kiểu cấu trúc dữ liệu sinhVien (struct)

```C
typedef struct sinhVien
{
    char maSV[20];
    char hoTen[50];
    float diemTB;
} sv; // Thay thế struct sinhVien thành sv để có thể tiện gọi.
```

### Khai báo cấu trúc của 1 node

```C
typedef struct node
{
    sv data; // 1 mắt xích (node) chính là một sinh viên, vậy 1 node sẽ phải mang kiểu sv.
    struct node *next; // Vì next cũng là 1 mắt xích, nên next sẽ mang kiểu node.
} node; // Thay vì gọi struct node thì gọi node hẳn là nhanh hơn đi =)).
```
### Khai báo cấu trúc của 1 list
Một node thì gọi là 1 mắt xích, vậy list coi như là sợi xích đi.
Muốn quản lý 1 danh sách liên kết, thì chúng ta sẽ cần 2 cái node, node đầu (head) và node cuối (tail).

```C
typedef struct
{
    node *head;
    node *tail;
    // Mắt xích đầu và mắt xích cuối, tầm này mà còn tự hỏi là sao lại kiểu node thì ăn đấm ngay.
} node;
```
### Hàm khởi tạo 1 node
Một struct sinhVien không phải là 1 node, vì 1 node thì chứa 1 struct sinhVien và 1 con trỏ *next.
Vậy chúng ta sẽ tạo 1 hàm, truyền vào 1 struct sinhVien và hàm sẽ trả ra 1 node mang data là sinh viên đó và 1 con trỏ next tới mắt xích tiếp theo.
```C
node *getNode(sv s) // Hàm sẽ trả ra 1 con trỏ node, truyền vào maSV, hoTen, diemTB của 1 sinh viên (s)
{
    node *p;
    p = (node*)malloc(sizeof(node)); // Cấp phát bộ nhớ cho node p
    if(p==NULL){
        printf("Cấp phát bộ nhớ thất bại"); // Khi máy đầy ram =)) Cơ mà máy giờ toàn 4, 8, 16GB thì làm cái thao tác này cho đầy đủ thôi.
    }else{ // Nếu cấp phát thành công.
        p->data = s; // data của p là dữ liệu của sinh viên truyền vào
        p->next = NULL; // vì đây chỉ là hàm khởi tạo mắt xích, chưa biết là cho cái mắt xích này vào vị trí nào của sợi xích.
    }
    return p;
}
```
### Hàm khởi tạo list ( Dây xích đấy =)) )
Mới học thì mình thắc mắc rằng, tại sao phải có đầu cuối trong khi mới khởi tạo thì làm gì có mắt xích nào ?
Node đầu (head) và node cuối (tail), xin nhắc lại là để quản lý danh sách liên kết.
Hàm khởi tạo list sẽ set cho đầu (head) và cuối (tail) thành NULL, vậy thì danh sách liên kết coi như không có mắt xích nào và chúng ta vẫn có thể sử dụng 2 node đó để quản lý.
```C
void init(list *l) // Nếu không hiểu tại sao lại truyền vào 1 con trỏ thì cần tìm hiểu lại tại post Con trỏ.
{
    l->head = NULL;
    l->tail = NULL;
}
```
Vậy là chúng ta đã tạo thành công 1 cấu trúc danh sách liên kết đơn. Phần tới là những thao tác cơ bản trên danh sách liên kết (Là rõ, biết tạo mà không biết thêm vào, xóa đi 1 mắt xích thì tạo làm gì chứ.)
## Những thao tác cơ bản trên Linked List

Trước tiên thì chúng ta cần tạo hàm nhập sinh viên.

```C
void nhap(sv *s)
{
    printf("Nhap ma sv: ");
    scanf("%s",&s->maSV);
    printf("Nhap ho ten: ");
    fflush(stdin);
    gets(s->hoTen);
    printf("Nhap diem TB: ");
    scanf("%f",&s->diemTB);
}
```

### Hàm chèn node vào đầu list

```C
void headInsert(list *l,node *p)
{
    if(l->head == NULL){ // Nếu list chưa có mắt xích nào, vậy head của list là NULL vì ở hàm khởi tạo list mình đã set head và tail = NULL.
        l->head = p; // Nếu list trống thì khi chèn p vào, p vừa là đầu (head) vừa là cuối (tail)
        l->tail = p;
    }else{ // Nếu list đã có mắt xích
        p->next = l->head->next; // Next của head sẽ trở thành next của p.
        l->head = p; // p sẽ thành head.
    }
}
```
### Hàm chèn node vào cuối list

```C
void tailInsert(list *l,node *p)
{
    if(l->head == NULL){ // Nếu list chưa có mắt xích nào, vậy head của list là NULL vì ở hàm khởi tạo list mình đã set head và tail = NULL.
        l->head = p; // Nếu list trống thì khi chèn p vào, p vừa là đầu (head) vừa là cuối (tail)
        l->tail = p;
    }else{ // Nếu list đã có mắt xích
        l->tail->next = p; // next của phần tử cuối cũ của list sẽ là p
        l->tail = p; // phần tử cuối mới của list là p
    }
}
```
### Hàm hiển thị list
```C
void xuat(list l)
{
    printf("%-10s%-30s%-20s\n","MaSv","Ho ten","Diem TB"); // Thao tác căn chỉnh thôi, đừng quá để ý
    int i=0;
    for(node *k=l.head; k!=NULL; k=k->next){
        i++;
        printf("%-10s%-30s%-20f\n",k->data.maSV,k->data.hoTen,k->data.diemTB);
    }
}
```
### Hàm tìm kiếm node theo mã sinh viên (maSV)
```C
node *search(list *l, char *msv)
{   //Tim theo MSSV

    for(node *p=l->head;p!=NULL;p=p->next){
        if(stricmp(p->data.ID,msv)==0){ // hàm stricmp() sẽ trả về 0 nếu 2 trường của nó cùng giá trị. Đại khái là so sánh 2 string.
            return p;
        }
    }
    return NULL;
}
```
### Hàm xóa node đầu
```C
void remove_head(list *l){
    node *tmp;
    if(l->head == NULL){
        return;
    }
    tmp = l->head;
    l->head = l->head->next;
    free(tmp);
}
```
### Hàm xóa 1 node bất kì
```C
void removeNode(list *l, char *k)
{
    node *p=l->head;
    node *q=NULL;
    while(p!=NULL)
    {
        if(stricmp(p->data.ID,k)==0) break;
        q=p;
        p=p->next;
    }
    if(p==NULL) printf("Khong tim thay");
    else if(q==NULL) remove_head(&l);
    else
    {
        q->next=p->next;
        if(q->next==NULL) l->tail=q;
        free(p);
    }
}
```
### Hàm sắp xếp tăng theo điểm TB
```C
void sortTang(list *l){
    sv tmp;
    if(l->head!=NULL){
        for(node *i=l->head; i!= NULL; i=i->next){
            for(node *j = i;j!=NULL;j=j->next){
                if(i->data.diemTB > j->data.diemTB){
                    tmp = i->data;
                    i->data = j->data;
                    j->data = tmp;
                }
            }
        }
    }
}
```
### Hàm sắp xếp giảm theo điểm TB
```C
void sortGiam(list *l){
    sv tmp;
    if(l->head!=NULL){
        for(node *i=l->head; i!= NULL; i=i->next){
            for(node *j = i;j!=NULL;j=j->next){
                if(i->data.diemTB < j->data.diemTB){
                    tmp = i->data;
                    i->data = j->data;
                    j->data = tmp;
                }
            }
        }
    }
}
```
### Tạo menu quản lý sinh viên
```C
int main(){
    list l;
    sv s;
    init(&l);
    int n,opt;
    char msnv[20];
    xuat(l);
    while(1){
        system("cls");
        printf("\n========== MENU ==========\n");
        printf("1. Tao danh sach sinh vien\n");
        printf("2. Hien thi danh sach sinh vien\n");
        printf("3. Xoa sinh vien\n");
        printf("4. Ket thuc\n");
        printf("Nhap lua chon: ");
        scanf("%d",&opt);
        switch(opt){
        case 1:
            printf("Nhap so sinh vien: ");
            scanf("%d",&n);
            for(int i=1;i<=n;i++){
                printf("Nhap SV thu %d: \n",i);
                nhap(&s);
                tailInsert(&l, getNode(s));
            }
            break;
        case 2:
            xuat(l);
            system("pause");
            break;
        case 3:
            printf("Nhap ma sinh vien can xoa: ");
            scanf("%s",&msnv);
            node *sResult = search(&l, msnv);
            if(sResult==NULL){
                printf("Khong tim thay sinh vien!");
            }else{
                removeNode(&l, msnv);
            }
            break;
        case 4:
            exit(1);
            break;
        }
    }
}
```

Full source code quản lý sinh viên: http://codepad.org/rglHLJ3z