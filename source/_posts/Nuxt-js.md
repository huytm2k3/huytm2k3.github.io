---
title: NuxtJS
date: 2023-3-13 8:51:00
tags:
---


## NuxtJS

- Như đã nói, Nuxt.js là một framework js để tạo các ứng dụng Universal Vue.js
- Là một framework, Nuxt.js có rất nhiều tính năng giúp bạn phát triển giữa phía client và server như Dữ liệu bất đồng bộ (Asynchronous Data), Middleware, Layouts, v.v.

## Tính năng

- Tạo ra file .vue (làm việc với vue)
- Automatic Code Splitting
- Server-Side Rendering
- Hệ thống router và dữ liệu bất đồng bộ
- Static File Serving
- Hỗ trợ ES6/ES7
- Đóng gói và nén js, css
- Quản lý các thẻ ở phần head (vue-meta)
- Hot reloading in Development
- Pre-processor: SASS, LESS, Stylus, etc

NuxtJS giống với create-react-app, cho phép tạo nhanh project VueJS với chuẩn cấu trúc Nuxt

## Getting started

### Khởi tạo dự án với npx create-nuxt-app

```bash
npx create-nuxt-app my-project
yarn create nuxt-app my-project
```
Notes: modules và linting tools nên chọn tất cả

```bash
yarn dev
npm run dev
```
### Cấu trúc thư mục trong NuxtJS

- Thư mục Assets Chứa những tài nguyên chưa được biên dịch như là LESS, SASS, hay JavaScript.
- Thư mục Components Chứa các components của vue.js
- Thư mục Layouts Chứa các layout (giao diện) cho ứng dụng
- Thư mục Middleware Chức Middleware của ứng dụng, middleware cho phép bạn định nghĩa các function được chạy trước khi render 1 page hoặc nhóm page.
- Thư mục Pages Thư mục này chứa các view của ứng dụng cũng như định nghĩa routes cho ứng dụng luôn.
- Thư mục Plugins Chức các javascript plugins
- Thư mục Static
Chứa các file tĩnh như các file ảnh chẳng hạn, được map tự động, ví dụ file /static/logo.png sẽ là yoursite/logo.png
- Thư mục Store Chứa các file của Vuex Store
- File nuxt.config.js Chứa các cấu hình được thiết đặt cho ứng dụng của bạn

### Thiết lập route trong Nuxt

Tạo file vue trong thư mục pages Nuxt sẽ tự tạo route theo tên của của file
Với các file route chứa param, sử dụng "_"
Ví dụ: _id.vue

```html
<template>
    {{ $route.params.id }}
</template>
```

nuxt-link dùng như Link-to trong React
navigate route với script:
```js
this.$router.push("url")
```
### Validate()

Phương thức xác thực trước khi render, ví dụ muốn kiểm tra _id truyền vào có 9-12 kí tự số:

```html
<template>
    {{ $route.params.id }}
</template>
<script>
export default {
    validate({ params }) {
        return /^[0-9]{9,12}$/.test(params.id)
    }
}
</script>
```

### Children component

Nếu khởi tạo 1 file settings.vue, 1 folder settings cùng cấp, vậy <nuxt-child /> của settings.vue sẽ nhận các route file trong settings làm con, điền vào <nuxt-child />

###  Layouts

Quản lý layout trong folder ./layout
Mặc định, các component sử dụng defaultlayout.vue có sẵn từ khi tạo project,

Để sử dụng layout tự tạo khác:

```html
<script>
    export default {
        layout: 'ten-layout'    
    }
</script>
```


