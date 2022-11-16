---
title: >-
  Làm ra một phần mềm chống gian lận thi cử như của một nhóm sinh viên Bách khoa
  có khó không?
date: 2022-11-16 23:50:13
tags:
---

Thông tin chi tiết bài viết về phần mềm đó trong link này: https://tuoitre.vn/3-sinh-vien-thu-nghiem-thanh-cong-phan-mem-chong-gian-lan-thi-cu-20220907161005997.htm

Người thường cũng có thể nhìn ra được, phần mềm này áp dụng AI - hay còn gọi là trí tuệ nhân tạo. Nhìn thì có vẻ nguy hiểm, không tốn khoảng thời gian tính bằng năm thì không thể làm ra được, nhưng thực chất cũng không khó khăn tới mức độ đó.

Để có thể detect các bộ phận trên cơ thể, mình sử dụng thư viện Mediapipe và OpenCV Python.

Mediapipe docs: https://google.github.io/mediapipe/
OpenCV docs: https://docs.opencv.org/4.x/

Mediapipe là thư viện giúp chúng ta detect các bộ phận, các điểm trên bộ phận.
OpenCV là thư viện giúp xử lý hình ảnh.

Vì mỗi điểm sẽ có 1 index xác định mà docs của Mediapipe đã nói rõ, nên việc chúng ta cần làm chỉ là đưa thuật toán vào, xử lý vị trí điểm, tính toán mức độ gian lận.

Theo mình, 3 features cần thiết của mediapipe để làm phần mềm này: 

![](/images/BackKhoaPost/Screenshot_1.png)

Lĩnh vực Trí tuệ nhân tạo (AI) và Thị giác máy tính (CV) là 2 lĩnh vực rất khó mà mình chưa dám đào sâu vào, ý tưởng thì có nhưng làm lại thứ họ đã làm thì chẳng vui vẻ gì. Post này nói chung.. tham khảo thôi, với lại truyền lửa cho các ITer có ý định học về 2 mảng này.
