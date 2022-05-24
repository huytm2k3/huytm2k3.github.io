---
title: HTTP Request trong Android (Java)
date: 2022-05-24 15:38:35
tags: [android, java]
---

## Mở đầu

Thông thường thì, muốn viết API kết nối tới server, Android không kết nối trực tiếp tới Database (MySQL, PostgreSQL, SQLite,...) mà phải thông qua web server, có thể dùng Volley của Java có sẵn, nhưng ở đây tôi sử dụng OkHTTP để làm chúng dễ dàng hơn.

Mọi thắc mắc xin liên hệ tới:
- Facebook: https://www.facebook.com/profile.php?id=100072417355186 (Tạ Minh Huy)
- Zalo: 0522566897
- Email: Huyat180522@gmail.com

## HTTP Request

Trước tiên, chèn dòng code này vào dependencies trong Gradle:

``` java
implementation("com.squareup.okhttp3:okhttp:4.9.3")
```

Và xin quyền Internet trong AndroidManifest:

``` html
<uses-permission android:name="android.permission.INTERNET" />
```

Sau đó Paste đoạn code này và sửa url cần GET:

``` java
OkHttpClient client = new OkHttpClient();

    String url = "https://jsonplaceholder.typicode.com/posts";

    Request request = new Request.Builder()
            .url(url)
            .build();

    client.newCall(request).enqueue(new Callback() {
        @Override
        public void onFailure(@NonNull Call call, @NonNull IOException e) {
            e.printStackTrace();
        }

        @Override
        public void onResponse(@NonNull Call call, @NonNull Response response) throws IOException {
            if(response.isSuccessful()){
                String myResponse = response.body().string();

                try {
                    // Code xử lý JSON được server trả về ...
                } catch (JSONException e) {
                    e.printStackTrace();
                }

                MainActivity.this.runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        // Code sau khi nhận được response ..
                    }
                });
            }
        }
    });
```

Kết quả là một chuỗi JSON: https://jsonplaceholder.typicode.com/posts

Khi nhận được một response là JSON, đó có thể là JSONObject, JSONArray, JSONArray Object, Nhưng thường sẽ là JSONArrayObject.

Tham khảo cách đọc một JSONArrayObject tại đây: http://huytm2k3.github.io/2022/05/24/JSONArray-Object-trong-Android/