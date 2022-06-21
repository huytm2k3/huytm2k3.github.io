---
title: Servlet/JSP
date: 2022-06-18 09:38:01
tags:
---

# Servlet

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

<!--more-->

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
<center>
<img src="../images/JavaServletPost/Screenshot_1.png">
</center>

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

Gần giống như config các class bình thường ở web.xml, web.xml có thể config cả filter.

```xml
<filter>
	<filter-name>logger</filter-name>
	<filter-class>com.huytm.filter.Logger</filter-class>
</filter>
  
<filter-mapping>
	<filter-name>logger</filter-name>
	<url-pattern>/servlet1</url-pattern>
</filter-mapping>
```

### Java config

Filter cũng có thể config bằng Java config như class. Dùng WebFilter để config UrlPatterns.
```java
package com.huytm.filter;

import java.io.IOException;

import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebFilter;

@WebFilter(urlPatterns= {"/servlet1"})
public class Logger implements Filter{

	@Override
	public void destroy() {
		// TODO Auto-generated method stub
		
	}

	@Override
	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
			throws IOException, ServletException {
		System.out.println("Filter 1");
		// TODO Auto-generated method stub
		chain.doFilter(request, response);
	}

	@Override
	public void init(FilterConfig filterConfig) throws ServletException {
		// TODO Auto-generated method stub
		
	}

}
```
### FilterConfig
Khởi tạo giá trị params giống trong Class Servlet.

## ServletContext

ServletContext có thể lưu và dùng cho tất cả các servlet như một biến trong 1 project.

Có thể dùng method
* getServletContext().setAttribute(key, value) để khởi tạo Servlet Context.
* getServletContext().getAttribute(key) để lấy giá trị Servlet Context.

Hoặc khởi tạo ServetContext trong Web.xml như thế này :
```xml
<context-param>
	<param-name>jdbc</param-name>
	<param-value>mysql</param-value>
</context-param>
```

Và khi đó, nhận giá trị bằng cách dùng method getServletContext.getInitParameter("jdbc");

## Auto refresh

Auto refresh trong Java Servlet sử dụng resp.setHeader("Refresh",time(s)) trong doGet.

Examlple:
```java
package com.huytm.servlet;

import java.io.IOException;
import java.io.PrintWriter;
import java.util.Date;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns= {"/auto-refresh"})
public class AutoRefresh extends HttpServlet{
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		resp.setContentType("text/html");
		
		resp.setHeader("Refresh","1");
		
		PrintWriter printWriter = resp.getWriter();
		
		printWriter.println("Thoi gian hien tai: " + new Date());
		
	}
}
```

## WelcomeFile tag trong Web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd" id="WebApp_ID" version="3.1">
  <display-name>JavaServletTest</display-name>
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>index.htm</welcome-file>
    <welcome-file>default.html</welcome-file>
    <welcome-file>default.jsp</welcome-file>
    <welcome-file>default.htm</welcome-file>
  </welcome-file-list>
  
</web-app>
```

Đây là những trang mặc định khi url chỉ gọi tới tên project (localhost:8080/DemoServlet)

Server sẽ tìm từng file có tên trong list từ trên xuống dưới, nếu tồn tại sẽ in ra trang web, nếu không sẽ trả về mã lỗi 404.

## Handle bắt lỗi

Khi trang web trả về một mã lỗi, thì server sẽ trả ra một giao diện tùy chỉnh chứ không phải là giao diện báo lỗi mặc định.

```xml
<error-page>
  	<error-code>404</error-code>
  	<location>/handle</location>
</error-page>
```
Khi gặp mã lỗi 404, server sẽ trả về trang có urlPatterns là "/handle".

# JSP

* JavaServlet Pages (JSP) công nghệ viết web động
* Sử dụng thẻ <% ... %> để viết code Java trong văn bản HTML
* JSP viết trên nền Java Servlet
* Giúp developer dễ dàng code và tích hợp nhiều modules

## Sử dụng

* <%...code Java...%> trong file jsp để chèn code Java vào trong HTML
* Code Java sẽ chạy trước để tạp ra kết quả kết hợp với code HTML của trang JSP
* <%=...expression Java...%> in ra giá trị trong Java thành HTML
* <%!...Khai báo Java...%> ít dùng
* <%--...Comment Java...%>
* Directives ảnh hưởng đến toàn cấu trúc của Servlet
* <%@include...%> bao gồm một ifle jsp khác
* <%@tablib...%> thêm một bộ thư viện vào file jsp cho việc sử dụng
* jsp:include bao gồm nội dung một file jsp khác

## Implicit Object

* request: là HttpServletRequest
* response: là HttpServletResponse
* out: là PrintWriter
* session: là HttpSession
* application: là ServletContext
* config: là ServletConfig

## Ví dụ Hello World

File Hello.jsp lưu tại folder webapp

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<p>Hello Boss!</p>
	
	<% 
		int x = 10;
		int y = 15;
		int z = x + y;
	%>
	
	<h1><%= z %></h1>
</body>
</html>
```

Cấu hình welcome-file thành file Hello.jsp tại web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd" id="WebApp_ID" version="3.1">
  <display-name>HelloJSP</display-name>
  <welcome-file-list>
    <welcome-file>Hello.jsp</welcome-file>
  </welcome-file-list>
</web-app>
```

## JSP Request

<% request.getParameter("id") %>

Example : Get param id từ url

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h1>Name: Ta Minh Huy</h1>
	<h2>Age: 19</h2>
	<h2>Sex: Male</h2>
	
	<% int id = Integer.valueOf(request.getParameter("id")); %>
	
	<p>Id cua ban la <%= id %></p>
	
</body>
</html>
```

## JSP Response

```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%
	response.sendRedirect("/HelloJSP/Hello.jsp");
%>
```

## JSP Form

Ví dụ phần này sẽ có 2 file JSP, 1 file addUser.jsp (Gửi form) và 1 file viewUser.jsp (Nhận form)

addUser.jsp:

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>

<h1>Them nguoi dung moi</h1>
<form action="viewUser.jsp" method="post">
	<input name="name" type="text" placeholder="Ten nguoi dung"/>
	<input name="password" type="password" placeholder="Mat khau"/>
	<input name="phone" type="text" placeholder="So dien thoai"/>
	<textarea rows="3" cols="3" name="about" placeholder="Gioi thieu"></textarea>
	<input name="favourites1" type="checkbox" value="Xem phim"/>
	<input name="favourites2" type="checkbox" value="Nghe nhac"/>
	
	<input type="submit" value="Add" />
</form>

</body>
</html>
```

viewUser.jsp

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<% 
		String name = request.getParameter("name");
		String password = request.getParameter("password");
		String phone = request.getParameter("phone");
		String favourites1 = request.getParameter("favourites1");
		String favourites2 = request.getParameter("favourites2");
	%>
	
	<table>
		<tr>
			<td>Ten</td> <td><%= name %></td>
		</tr>
		<tr>
			<td>Mat khau</td> <td><%= password %></td>
		</tr>
		<tr>
			<td>So dien thoai</td> <td><%= phone %></td>
		</tr>
		<tr>
			<td>Xem phim</td> <td><%= favourites1 %></td>
		</tr>
		<tr>
			<td>Nghe nhac</td> <td><%= favourites2 %></td>
		</tr>
	</table>
</body>
</html>
```
