---
title: Realtime Chat App với NodeJS Socket.io
date: 2022-11-30 08:18:27
tags:
---


## Introduce

![](/images/SocketIONodeJS/Screenshot_1.png)

Ngày trước khi người ta chưa sử dụng Socket, muốn tạo 1 app chat realtime có 2 cách là Polling và Long Polling

Polling là client sau mỗi khoảng thời gian sẽ gửi 1 request lên để lấy dữ liệu, nếu không có dữ liệu mới Server sẽ trả về dữ liệu cũ hoặc không trả về gì.

Long Polling có nghĩa là, client sẽ gửi 1 request và đợi cho tới khi server có dữ liệu mới, server sẽ trả về dữ liệu mới đó.

Cả 2 cách trên đều không realtime.

Streaming tức là client sẽ gửi 1 subscribe như 1 thông tin đăng ký, khi này mỗi khi có dữ liệu mới, server sẽ gửi về cho client.

## Tạo server với ExpressJS + socket.io + EJS

```js
const express = require("express");
const app = express();

const http = require("http");
const server = http.createServer(app);

const { Server } = require("socket.io");

const io = new Server(server);

{
  // Template engine ejs
  app.engine(".html", require("ejs").__express);
  app.use(express.static("public"));
  app.set("view engine", "html");
}

app.get("/", (req, res) => {
  res.render("index", {});
});

io.on("connection", (socket) => {
  console.log("user connected");
});

server.listen(8080, () => {
  console.log("App running on http://localhost:8080");
});
```

Thao tác nhận kết nối của server từ client

```js
io.on("connection", (socket) => {
  console.log("user connected");
});
```

Mỗi khi có 1 user gửi socket tới, sẽ hiện ra dòng log 'user connected'

Khi này, client sẽ kết nối:

```js
const socket = io();
```

Để gửi data, sử dụng method emit:

```js
socket.emit("on-chat", {
  message: $("#txt-message").val(),
});
```

Với on-chat là keyword, khi này server sẽ đón data bằng cách:

```js
socket.on("on-chat", (arg) => {
  console.log(arg);
});
```

Và dĩ nhiên, server cần phải gửi ngược lại phần tin nhắn, để mọi người đều nhận được và cập nhật tin nhắn được gửi từ người khác

```js
socket.on("on-chat", (arg) => {
  console.log(arg);
  io.emit("user-chat", arg);
});
```

Lúc này, client sẽ đón lại data từ phía server gửi về:

```js
socket.on("user-chat", (arg) => {
  console.log(arg);
});
```

Mô hình gửi nhận sẽ tóm gọn lại như này: 1 user sẽ gửi lên tin nhắn kèm theo socket keyword là 'on-chat', server sẽ sử dụng keyword đó để đón lấy tin nhắn và gửi lại cho tất cả các user kèm 1 keyword khác là 'user-chat', lúc này tất cả user dùng keyword 'user-chat' để lấy tin nhắn và hiển thị ra.

Project cờ caro 2 người online mình làm bằng Socket.io: https://github.com/huytm2k3/carogame