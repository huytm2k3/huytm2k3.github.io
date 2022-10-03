---
title: Java Spring Boot trong 2 giờ!
date: 2022-09-23 15:28:54
tags: [java, spring-boot, servlet, jsp]
---

## Mục tiêu bài viết
- Tạo được request GET, POST, PUT, DELETE Rest API với Java Spring
- Làm việc với các khái niệm Repositories, Dependency Injection và truy cập dữ liệu trong CSDL MySQL với Docker Container
- Service Injection, viết Rest controller cho phép upload file lên server
## Lets go!

Để học Spring boot, chúng ta phải hiểu được cách thức hoạt động của mô hình MVC, trước đó tôi đã từng viết 1 bài về mô hình này.

Các class trong package controller nên có:

```java
@RestController
@RequestMapping(path = "/api/v1/Products")
```
Nếu ai học JSP/Servlet rồi thì hẳn biết cái này.

Tạo 1 method GET

```java
package com.tutorial.apidemo.Springboot.tutorial.controllers;


import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;

@RestController
@RequestMapping(path = "/api/v1/Products")

public class ProductController
{
    @GetMapping("")
    List<String> getAllProducts() {
        return List.of("iphone", "ipad");
    }
}

```
