---
title: JSONArray Object trong Android
date: 2022-05-24 15:49:46
tags: [android, java]
---

## Mở đầu
Ngày trước, người ta thường trả và đọc dữ liệu bằng file XML. Nhưng ngày nay, JSON trở nên thông dụng và dễ dàng hơn khi làm việc đó. Vậy JSON là gì?

JSON là viết tắt của JavaScript Object Notation, là một kiểu định dạng dữ liệu tuân theo một quy luật nhất định mà hầu hết các ngôn ngữ lập trình hiện nay đều có thể đọc được. JSON là một tiêu chuẩn mở để trao đổi dữ liệu trên web.

Mọi thắc mắc xin liên hệ tới:
- Facebook: https://www.facebook.com/profile.php?id=100072417355186 (Tạ Minh Huy)
- Zalo: 0522566897
- Email: Huyat180522@gmail.com

## Xử lý JSON trong Android (Code Java)

Trong bài trước (Nếu ai chưa xem qua thì có thể kéo xuống, link bài viết mình để ở phần mô tả) chúng ta đã dùng HTTP Request để nhận về một JSONArray Object. Giờ chúng ta hãy cùng xử lý nó.

JSONArray Object: 
``` json
[
  {
    "userId": 1,
    "id": 1,
    "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
    "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
  },
  {
    "userId": 1,
    "id": 2,
    "title": "qui est esse",
    "body": "est rerum tempore vitae\nsequi sint nihil reprehenderit dolor beatae ea dolores neque\nfugiat blanditiis voluptate porro vel nihil molestiae ut reiciendis\nqui aperiam non debitis possimus qui neque nisi nulla"
  },
  {
    "userId": 1,
    "id": 3,
    "title": "ea molestias quasi exercitationem repellat qui ipsa sit aut",
    "body": "et iusto sed quo iure\nvoluptatem occaecati omnis eligendi aut ad\nvoluptatem doloribus vel accusantium quis pariatur\nmolestiae porro eius odio et labore et velit aut"
  },
  {
    "userId": 1,
    "id": 4,
    "title": "eum et est occaecati",
    "body": "ullam et saepe reiciendis voluptatem adipisci\nsit amet autem assumenda provident rerum culpa\nquis hic commodi nesciunt rem tenetur doloremque ipsam iure\nquis sunt voluptatem rerum illo velit"
  }...
]
```

Vậy cùng nói qua tiến trình thực hiện nhé, mục tiêu của mình là sẽ tạo một ArrayList chứa nhiều object (Chứa các trường: userId, id, title, body), request về thì tự động lưu vào ArrayList đó để sau này có thể sử dụng.

Vậy trước tiên, hãy tạo một class Post với đầy đủ Constructor, Getters and Setter gồm các trường trên :

```java
package mhuy.com.okhttpexample;

public class Post {
    private int userId;
    private int id;
    private String title;
    private String body;

    public Post(int userId, int id, String title, String body) {
        this.userId = userId;
        this.id = id;
        this.title = title;
        this.body = body;
    }

    public int getUserId() {
        return userId;
    }

    public void setUserId(int userId) {
        this.userId = userId;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public String getBody() {
        return body;
    }

    public void setBody(String body) {
        this.body = body;
    }
}
```
Nhớ import vào MainActivity.

Sau đó, trong code Request, hãy xử lý Response như sau:

```java
client.newCall(request).enqueue(new Callback() {
    @Override
    public void onFailure(@NonNull Call call, @NonNull IOException e) {
        e.printStackTrace();
    }

    @Override
    public void onResponse(@NonNull Call call, @NonNull Response response) throws IOException {
        if(response.isSuccessful()){
            String myResponse = response.body().string();
            // Tạo ArrayList với kiểu dữ liệu Post
            ArrayList<Post> posts = new ArrayList<>();

            try {

                // Tạo JSONArray
                JSONArray array = new JSONArray(myResponse);

                for(int i=0; i<array.length();i++){
                    // Và duyệt từng JSONObject trong JSONArray
                    JSONObject object = array.getJSONObject(i);

                    int userId = object.getInt("userId");
                    int id = object.getInt("id");
                    String title = object.getString("title");
                    String body = object.getString("body");


                // Thêm vào ArrayList
                posts.add(new Post(userId, id, title, body));

                }
            } catch (JSONException e) {
                e.printStackTrace();
            }

            MainActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    tvResult.setText(myResponse);
                    Toast.makeText(MainActivity.this, monhoc, Toast.LENGTH_SHORT).show();
                    for(Post post: posts){
                        // Này là hiển thị để kiểm tra.
                        Log.d("test", String.valueOf(post.getTitle()));
                    }
                }
            });
        }
    }
});
```

## Description

Link bài trước: http://huytm2k3.github.io/2022/05/24/HTTP-Request-trong-Android-Java/


Thanks for all <3 !
