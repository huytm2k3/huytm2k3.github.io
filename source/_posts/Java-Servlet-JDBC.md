---
title: Java Servlet JDBC
date: 2022-06-24 09:49:37
tags: [java, servlet/jsp, JDBC]
---

## Giới thiệu

Hiện nay hầu hết các ứng dụng Java hay các framework của nó đều dần chuyển sang các ORM(Object Relational Mapping) để làm việc với database, có thể kể đến là hibernate được sử dụng rộng rãi. Thế nên mọi người có xu hướng dần quên đi JDBC, thế nhưng các bạn có biết rằng bên dưới hibermate đang sử dụng JDBC để để kết nối đến database và thực thi các lệnh SQL được nó tạo ra. Back to basic, cùng tìm hiểu JDBC là gì nha.

JDBC là viết tắt của Java Database Connectivity là một API dùng để kết nối và thực thi các câu lệnh SQL xuống database. JDBC API sử dụng JDBC driver để làm việc với database gồm 4 loại.

- JDBC-ODBC Bridge Driver
- Native Driver
- Network Protocol Driver
- Thin Driver

Phần tutorial này mình sẽ hướng dẫn các bạn kết nối tới Postgresql, với những CSDL khác thì làm khá giống, chỉ là thay đổi 1 số file jar trong Library mà thôi.

## Tải và thêm Driver vào Lib

Tạo một DynamicWebProject.

Truy cập vào : https://jdbc.postgresql.org/download/postgresql-42.4.0.jar để download Postgresql JDBC Driver.

Chuột phải vào Project, chọn Build Path/Configure Build Path/Java Build Path/Libraries/Classpath.
Sau đó ấn vào Add External JARS và chọn File jar vừa tải được.

Cuối cùng thì hãy kéo thả file Jar vừa tải được vào thư mục /src/main/webapp/WEB-INF/lib

## Các Class.

Chúng ta sẽ dùng mô hình MVC, tạo 2 package là "controller" và "model".

Trong Package model sẽ có 2 class là DAL.java và DBProduct.java

- Class DAL: Dùng để kết nối tới Database, lấy dữ liệu dưới dạng "ResultSet".
- Class DBProduct: Dùng để truy vấn Sql.

Trong /src/main/webapp có một file JSP ShowProduct để hiển thị dữ liệu

Trong Package controller có 1 class là DisplayProduct.java, để lấy dữ liệu từ DBProduct truy vấn Sql và đổ vào ShowProduct.jsp/

### Class DAL.java

```java
package com.mhuy.model;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class DAL {
	Connection conn;
	Statement stsm;

	public DAL() {
		try {
			
			System.out.println("TEST");
			
			Class.forName("org.postgresql.Driver");
			conn = DriverManager.getConnection("jdbc:postgresql://localhost:5432/huyshop", "postgres", "2003");
			
			System.out.println(conn);

			if (conn != null) {
				System.out.println("Connection OK");
			} else {
				System.out.println("Failed");
			}

		} catch (Exception e) {
			System.out.println(e);
		}
	}

	public ResultSet getData(String sql) {
		stsm = null;
		try {
			stsm = conn.createStatement();
			return stsm.executeQuery(sql);
		} catch (SQLException e) {
			e.printStackTrace();
		}
		return null;
	}

	public boolean updateData(String sql) {
		stsm = null;
		try {
			stsm = conn.createStatement();
			return stsm.executeUpdate(sql) > 0 ? true : false;
		} catch (SQLException e) {
			e.printStackTrace();
		}

		return false;

	}

}
```

### Class DBProduct

```java
package com.mhuy.model;

import java.sql.ResultSet;

public class DBProduct {
	
	DAL dal;
	
	public DBProduct() {
		dal = new DAL();
	}
	
	public ResultSet getListProduct() {
		return dal.getData("SELECT * FROM san_pham");
	}

}
```

### Class DisplayProduct

```java
package com.mhuy.controller;

import java.io.IOException;
import java.sql.ResultSet;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.mhuy.model.DbProduct;

@WebServlet("/DisplayProduct")
public class DisplayProduct extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    public DisplayProduct() {
        super();
    }
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		
		System.out.println("TEST");
		
		DbProduct dbProduct = new DbProduct();
		ResultSet rs = dbProduct.getListProduct();
		
		System.out.println("TEST");
		
		request.setAttribute("rs", rs);
		request.getRequestDispatcher("ShowProduct.jsp").forward(request, response);;
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

		doGet(request, response);
	}

}
```

### ShowProduct.jsp

```html
<%@page import="java.sql.ResultSet"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Product List</title>
</head>
<body>
<%
	ResultSet rs = (ResultSet) request.getAttribute("rs"); 
%>

<% while(rs.next()) { %>
<h4><%= rs.getString(3) %></h4>
<%} %>

</body>
</html>
```

