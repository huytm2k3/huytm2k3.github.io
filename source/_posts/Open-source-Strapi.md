---
title: Open source Strapi
date: 2022-04-25 16:33:26
tags: [strapi, nodejs]
categories: [Back-end]
---
## Mở đầu

Source:
https://viblo.asia/p/lam-blog-voi-strapi-va-nextjs-tai-sao-lai-khong-gDVK260wKLj
https://docs.strapi.io/developer-docs/latest/getting-started/quick-start.html#_1-install-strapi-and-create-a-new-project

Bài viết này mình sẽ tóm tắt lại cách cài đặt và sử dụng Open source Strapi. Vậy trước hết, strapi là gì? 

Strapi là gì, nó open source, một framework NodeJS giúp bạn quản lí nội dung CMS một cách dẽ dàng và xây dựng sẵn các Rest full API cũng như khả năng custom API. Giúp chúng ta tiết kiệm hàng tuần hàng tháng phát triển.

## Installation

### Tạo một project với Strapi

#### Bước 1: 

Chạy dòng lệnh dưới ở Terminal:

``` PowerShell
npx create-strapi-app@latest my-project --quickstart
```
#### Bước 2:

Sau khi cài đặt xong, trình duyệt của bạn tự động mở 1 tab mới.

Hãy đăng kí tài khoản đầu tiên (Tài khoản với quyền admin đầu tiên). Bây giờ bạn có quyền truy cập vào Admin panel:

![](/images/strapiPost/Screenshot_1.png)

### Xây dựng nội dung

#### Bước 1: Tạo Collection types với Content-type Builder

##### Tạo Collection type Restaurant

![](https://docs.strapi.io/assets/img/qsg-handson-restaurant_2.28faf048.gif)

##### Tạo Collection type Category

Tạo Collection type Category với 1 trường "name" (Text) và một trường Relation field

![](https://docs.strapi.io/assets/img/qsg-handson-part2-02-collection_ct.1520deb7.png)

Sau đó click vào nút Save


<!--more-->

#### Bước 2: Sử dụng Collection type để tạo các Entries mới

##### Add Restaurant

1. Đi tới Content Manager > Collection types - Restaurant ở navigation
2. Click vào Add new entry
3. Nhập tên Restaurant và Description (Mô tả)
4. Save

![](https://docs.strapi.io/assets/img/qsg-handson-part2-03-restaurant.a35be858.png)

##### Add Categories

1. Đi tới Content Manager > Collection types - Category
1. Click vào Add new entry
2. Nhập French Food ở trường Name
3. Save
4. Quay trở lại Category, sau đó click lại vào Add new entry
5. Nhập Brunch ở trường name, sau đó lưu.

![](https://docs.strapi.io/assets/img/qsg-handson-categories.b623cafc.gif)

##### Thêm Category cho 1 Restaurant

Đi tới Content Manager > Collection types - Restaurant ở Navigation, và click vào "Biscotte Restaurant"
Ở Sidebar bên phải, ở Categories drop-down list, chọn "Brunch". Bấm Save

#### Bước 3: Set Roles & Permissions

1. Click vào General Setting ở dưới của main navigation
2. Dưới Users & Permissions Plugin, chọn Roles
3. Click vào Public role
4. Cuộn xuống Permissions
5. Ở Permission Tab, tìm Restaurant và click vào nó
6. Click vào Find và Findone
7. Lặp lại với Category
8. Save

![](https://docs.strapi.io/assets/img/qsg-handson-part2-04-roles.ba3d34a5.png)

#### Bước 4: Publish nội dung

Đầu tiên, truy cập tới Content Manager > Collection types - Category.
1. Click vào Brunch
2. Publish
3. Trong cửa sổ Confirmation, Click Yes, publish
Sau đó lặp lại với French Food
Cuối cùng là publish Restaurant
![](https://docs.strapi.io/assets/img/qsg-handson-publish.1093c516.gif)

#### Bước 5: Sử dụng API

Truy cập tới http://localhost:1337/api/restaurants