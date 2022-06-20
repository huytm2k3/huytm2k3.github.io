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
## Class PersonSev:
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
## Redirect chuyển hướng trang web trong java
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
## Java servlet Cookies
### Cookie là gì?
* Cookie là một file text lưu ở phía browsers của client
* Cookie lưu thông tin dạng key/value
* Request sẽ gửi thông tin cookies trong header mỗi lần gọi
* Java Servlet hỗ trợ http cookie
* Có thời gian sống xác định

Giờ tôi sẽ tạo 2 class ví dụ là Servlet1 (Class addCookie) và Servlet2(Class getCookie)

### Tạo Cookies
Class Servlet 1:

```java
package com.huytm;
import java.io.IOException;
import java.io.PrintWriter;
import java.net.URLEncoder;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns= {"/servlet1"})
public class Servlet1 extends HttpServlet{
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		resp.setContentType("text/html");
		
		PrintWriter printWriter = resp.getWriter();
		
		printWriter.println("Xin chao Ta Minh Huy");
		
		Cookie cookie = new Cookie("ten", URLEncoder.encode("ta minh huy","UTF-8"));
		
		cookie.setMaxAge(1000);
		
		resp.addCookie(cookie);
		
		
	}
}
```

### Get Cookies
Class Servlet2

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

@WebServlet(urlPatterns= {"/servlet2"})
public class Servlet2 extends HttpServlet{
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		resp.setContentType("text/html");
		
		PrintWriter printWriter = resp.getWriter();
		
		Cookie[] cookies = req.getCookies();
		
		for(Cookie c : cookies) {
			printWriter.println(c.getName() + ": " + c.getValue() + "<br/>");
		}
	}
}
```

[ ] Lưu ý: Cookies không thể lưu được kí tự trắng, vì vậy bắt buộc phải dùng UrlEncode.

### Xóa cookies

```java
if(c.getName().equals("ages")){
	c.setMaxAge(0);
	
	resp.addCookie(c);
}
```

## Login - Servlet Cookies

Ví dụ phần này là khi người dùng nhập đúng username và password, sẽ Redirect về một trang web "Welcome" - Lưu cookie, còn nếu sai thì quay trở lại trang Login.

Class Login
```java
package com.huytm.authen;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns= {"/login"})
public class Login extends HttpServlet{
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		resp.setContentType("text/html");
		PrintWriter printWriter = resp.getWriter();
		
		printWriter.println("<form action = '/JavaServletTest/login' method='post'>");
		printWriter.println("Username: <input type='text' name='username'/>");
		printWriter.println("Password: <input type='password' name='password' />");
		printWriter.println("<input type='submit' value='Login' />");
		printWriter.println("</form>");
		
		printWriter.close();
	}
	
	@Override
	protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		resp.setContentType("text/html");
		
		String username = req.getParameter("username");
		String password = req.getParameter("password");
		
		if(username.equals("admin") && password.equals("123456")) {
			
			Cookie cookie = new Cookie ("username", username);
			cookie.setMaxAge(30);
			
			resp.addCookie(cookie);
			resp.sendRedirect("/JavaServletTest/welcome");
		}else {
			resp.sendRedirect("/JavaServletTest/login");
		}
		
		
	}
	
}
```
Class Welcome
```java
package com.huytm.authen;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns = {"/welcome"})
public class Welcome extends HttpServlet{
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		resp.setContentType("text/html");
		
		PrintWriter printWriter = resp.getWriter();
		
		String username = "";
		
		Cookie[] cookies = req.getCookies();
		
		for(Cookie c: cookies) {
			if(c.getName().equals("username")) {
				username = c.getValue();
			}
		}
		
		printWriter.println("Xin chao " + username);
	}
}
```
## Java Servlet Session

### Giao thức HTTP
![](/images/JavaServletPost/Screenshot_1.png)
### Cách hoạt động
* Cookies
Set ID vào Cookie để nhận dạng
* Hidden Field trong Form
Set id vào một trường ẩn trong form
```html
<input type="hidden" name="sessionid" value="12345">
```
* Url Rewriting
http:/tutorialspoint.com/file.html;sessionid=12345

### HttpSession
* Là một interface trong Servlet giúp lưu các thông tin người dùng qua các servlet khác nhau.
```java
HttpSession session = request.getSession();
```
Cũng khá giống với cookie, cũng là setAttributes(name, value) và getSession
Ví dụ lần này là class Session1 (Đặt giá trị Session) và class Session2 (Lấy giá trị Session và in ra màn hình).

Class Session1
```java
package com.mhuy.session;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

@WebServlet(urlPatterns= {"/hello-session"})
public class Session1 extends HttpServlet{
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		HttpSession httpSession = req.getSession();
		
		httpSession.setAttribute("name", "taminhhuy");
		
		resp.setContentType("text/html");
		
		PrintWriter printWriter = resp.getWriter();
		
		printWriter.println("Xin chao taminhhuy");
		
	}
}
```
Class Session2
```java
package com.mhuy.session;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

@WebServlet(urlPatterns = {"/session-2"})
public class Session2 extends HttpServlet{
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		resp.setContentType("text/html");
		
		PrintWriter printWriter = resp.getWriter();
		
		String name = "";
		
		HttpSession httpSession = req.getSession();
		
		Object obj = httpSession.getAttribute("name");
		
		if(obj != null) {
			name = String.valueOf(obj);
		} else {
			resp.sendRedirect("/JavaServletSession/hello-session");
		}
		
		printWriter.println("Xin chao: " + name);
		
	}
}
```
## Filter

* Filter là một đối tượng dùng để xử lý request trươc khi gọi đến một servlet đích, và response trả về kết quả từ servlet.
* Dùng nhiều filter một lúc
* Dễ dàng tích hợp bất cứ lúc nào

### Tác dụng của filter

* Login
* Check ip
* Nén file
* Validate dữ liệu
* ...

### XML config