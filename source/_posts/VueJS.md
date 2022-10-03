---
title: VueJS
date: 2022-09-22 13:39:32
tags: [front-end, vuejs]
---

## VueJS là gì?

VueJS được phát triển bởi một nhân viên cũ của Google. Tài trợ bởi Laravel
Có những khái niệm giống với React, có một số tính năng giống với Angular1
VueJS có thể tích hợp được bất kì trang web nào (Có thể sử dụng vào 1 phần nhỏ của trang web)

## Single-Page Application

Cái này giống trong React, chuyển trang chỉ cần load những component cần thiết.

## Môi trường lập trình

- Visual Studio Code
- NodeJS
- NPM
- Github

## Getting Started

### Cài đặt
### Vue Instance
#### Data
Javascript:
```js
var vueInstance = new Vue({
    el: '#app', // Element selector
    data: {
        title: 'Điện thoại Samsung'
    }
})

console.log(vueInstance);
```
Html code Template syntax:
```html
<div id="app">
    <p>{{title}}</p>
</div>
```

Hệ thống Reactivity: Khi title thay đổi, các element có title sẽ được reload

```js
vueInstance.title = 'Dien thoai Oppo'
```

#### Methods
```js
var vueInstance = new Vue({
    el: '#app' , // Element selector
    methods: {
        say: function(text){
            return 'Hello ' + text;
        }
    }
})
```

```html
<div id="app">
    <p>{{say('World')}}</p>
</div>
```
Dùng this để chỉ chính nó. Ví dụ muốn lấy title trong methods của Vue Instance
```js
var vueInstance = new Vue({
    el: '#app' , // Element selector
    data: {
        title: 'Tieu de 1'
    },
    methods: {
        say: function(text){
            console.log(this.title)
        }
    }
})
```

### Data Binding

Khi ràng buộc dữ liệu vào thuộc tính của thẻ, không được dùng trực tiếp như href="{{url}}", mà phải dùng v-bind:
```html
<a v-bind:href="url">{{}}</a>
```

Chỉ sử dụng được các toán tử đơn giản trong Template Syntax.
Không sử dụng được khai báo biến, flow control, phải sử dụng toán tử 3 ngôi 
```js
( {{ true ? 'OK' : 'Not OK' }} )
```

### Event Handling

Thay vì onclick trong Html, Vue sử dụng v-on:click

```html
<div id="app">
    <button v-on:click="counter += 1">Add 1</button>
    <p>{{counter}}</p>
</div>
```
```js
var vueInstance = new Vue({
    el: '#app' , // Element selector
    data: {
        counter: 0
    }
})
```

### Two way binding

Thay vì sử dụng việc ràng buộc 2 chiều phức tạp như trong React, Angular bằng cách e.target.value thì trong VueJS chúng ta có v-model

https://www.youtube.com/watch?v=7fKenz7ozj4&list=PLv6GftO355AtDjStqeyXvhA1oRLuhvJWf&index=10

### Ràng buộc class

Vì multi-class luôn cách nhau bởi dấu cách, vậy nếu v-on:class cộng chuỗi thì không hề dễ nhìn chút nào.

VueJS hỗ trợ class Object

https://www.youtube.com/watch?v=8BHDy7Kb8eQ&list=PLv6GftO355AtDjStqeyXvhA1oRLuhvJWf&index=11

### Render Template với biểu thức điều kiện

https://www.youtube.com/watch?v=xZrioi3zOP4&list=PLv6GftO355AtDjStqeyXvhA1oRLuhvJWf&index=13

### Render Template với loop

https://www.youtube.com/watch?v=bCOcZ_BMaJU&list=PLv6GftO355AtDjStqeyXvhA1oRLuhvJWf&index=14

### Render Template với ngoài loop trong condition 

https://www.youtube.com/watch?v=gd-9xTlT6b4&list=PLv6GftO355AtDjStqeyXvhA1oRLuhvJWf&index=15

### Lưu ý quan trọng về Array và Object trong VueJS

- So sánh "===" trong JS là so sánh địa chỉ, không phải so sánh phần tử
- Thay đổi, thêm phần tử vào array hoặc object bằng index thì Reactivity của Vue không hoạt động, cần sử dụng hàm có sẵn của VueJS

```js
app.$set(p1, p2)
app.$set(p1, p2, p3)
```

https://www.youtube.com/watch?v=h7ReovfFZYA&list=PLv6GftO355AtDjStqeyXvhA1oRLuhvJWf&index=17

### Vue CLI(Command line interface) Installation

https://github.com/vuejs-templates/webpack