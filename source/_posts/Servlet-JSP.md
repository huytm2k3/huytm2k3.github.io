---
title: Servlet/JSP
date: 2022-06-18 09:38:01
tags:
---
Java Servlet/JSP
## Requirement
	Java EE Eclipse
## Installation
	 
## Ví dụ Hello Servlet
Tạo một Dynamic Web Project kèm theo web.xml
Tạo một package tại thư mục src, và một Class HelloServlet nằm trong package đó, extends HttpServlet
 
Override và sửa một số method
 
```java
package com.huytm;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class HelloServlet extends HttpServlet{

	@Override
	public void init() throws ServletException {
		System.out.println("Start Servlet");
	}
	@Override
	public void destroy() {
		System.out.println("Stop servlet");
	}
	
	@Override
	protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		// TODO Auto-generated method stub
		super.service(req, resp);
		
		System.out.println("Phuong thuc cua request " + req.getMethod());
	}
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		// TODO Auto-generated method stub
		resp.setContentType("text/html");
		PrintWriter writer = resp.getWriter();
		
		writer.println("<h1>Xin chao servlet - HuyTM</h1><p>AAA</p>");
		writer.close();
	}
	
}

```

Cấu hình tại web.xml:
 
Khởi chạy server:
1.	Chuột phải vào server Tomcat, chọn Add and remove, chọn class cần add
 
2.	Chuột phải vào server, chọn Clean…
3.	Start server
 
## Cấu hình Java Servlet bằng Java Annotation
 
	Thay vì phải cấu hình tại web.xml, ta dùng annotation cấu hình ngay tại class.

## Servlet Request

```java
package com.huytm;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns= {"/get-request"})

public class GetRequestDemo extends HttpServlet{
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		// TODO Auto-generated method stub
		resp.setContentType("text/html");
		
		PrintWriter printWriter = resp.getWriter();
		
		printWriter.println("Test");
		
		String ten = req.getParameter("ten");
		
		printWriter.println("Xin chao " + ten);
	}
}

```
 
## Servlet Response

```java
package com.huytm;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns = {"/response-demo"})

public class ResponseServletDemo extends HttpServlet{
	
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		
		resp.setContentType("text/html");
		
		PrintWriter printWriter = resp.getWriter();
		
		printWriter.println("<h1>Xin chao Ta Minh Huy</h1>");
		
		printWriter.println("<h1>Xin chao Ta Minh Huy</h1>");
		
	}

}

```

## Servlet Config
 
## Response Code trong Java Servlet

```java
package com.huytm;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns= {"/test-code"})

public class CodeServlet extends HttpServlet{
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		// TODO Auto-generated method stub
		resp.setContentType("text/html");
		
		resp.sendError(404);
		
	}
}
```

Khi này, server trả về mã lỗi là 404.
 
## Đọc dữ liệu gửi lên từ Client qua URL trong Java Web
```java
package com.huytm;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns= {"/get-request"})

public class GetRequestDemo extends HttpServlet{
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		// TODO Auto-generated method stub
		resp.setContentType("text/html");
		
		PrintWriter printWriter = resp.getWriter();
		
		printWriter.println("Test");
		
		String ten = req.getParameter("ten");
		
		printWriter.println("Xin chao " + ten);
	}
}
```

Khi này, client truyền vào Param tại url, Server get Param với tên là “ten”, và in ra dòng Xin chao + <ten>
## POST GET method in Servlet Java
Ví dụ này là tạo 2 Class, 1 class chứa form để post dữ liệu lên, và một class dùng để Get dữ liệu hiển thị ra trang web.

Ở đây tôi có 2 class là FormPerson (Class để gửi form), PersonSev (Class để nhận form). FormPerson sẽ dùng doGet, PersonSev dùng doPost.
Class FormPerson:
```java
package com.huytm;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns={"/user-form"})

public class FormPerson extends HttpServlet{
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		resp.setContentType("text/html");
		
		PrintWriter printWriter = resp.getWriter();
		
		printWriter.println("<form action='/DemoServlet/user' method='POST'>");
		printWriter.println("Ten: <input type='text' name='ten'/>");
		printWriter.println("Tuoi: <input type='text' name='tuoi'/>");
		printWriter.println("Dia chi: <input type='text' name='diaChi'/>");

		printWriter.println("<input type='submit' />");

		printWriter.println("</form>");
	}
}
```
Class PersonSev:
```java
package com.huytm;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns= {"/user"})

public class PersonSev extends HttpServlet{
	@Override
	protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		// TODO Auto-generated method stub
		resp.setContentType("text/html");
		
		PrintWriter printWriter = resp.getWriter();
		
		String ten = req.getParameter("ten");
		String tuoi = req.getParameter("tuoi");
		String diaChi = req.getParameter("diaChi");
		
		
		printWriter.println(ten + tuoi + diaChi);
	}
}
```
Redirect chuyển hướng trang web trong java
```java
package com.huytm;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns= {"/redirect"})
public class RedirectServlet extends HttpServlet{
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		resp.sendRedirect("http://huytm2k3.github.io");
	}
}

```


