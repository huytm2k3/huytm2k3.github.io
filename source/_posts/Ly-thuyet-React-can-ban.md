---
title: Lý thuyết React căn bản
date: 2023-02-23 09:48:58
tags:
---

<b>Component: </b> Chia nhỏ UI, tái sử dụng, xử lý từng phần riêng biệt (Class component, functional component)
<b>Props: </b> Component cũng giống function trong JS, nên có thể nhận các tham chiếu đầu vào
<b>State: </b> Kho lưu trữ dữ liệu trong React
<b>LifeCycle: </b> Vòng đời (Mounting, Updating, Unmounting)
<b>Handling Events: </b> CamelCase, sử dụng hàm thay vì chuỗi
<b>Conditional rendering: </b> Render theo điều kiện
<b>List, key: </b> Key giúp React định danh các phần tử trong list, giúp thêm sửa xóa dễ hơn
<b>Context: </b> Truyền dữ liệu qua cây thành phần mà không cần truyền props thủ công
<b>Error Boundaries: </b>Giống try catch
<b>useRef: </b> Truy cập vào DOM nodes hoặc React elements trong phương thức render
<b>Higher-order component: </b>Hàm lấy về 1 element và trả 1 element mới
<b>Fragment: </b> Gom gói các element con để return
<b>Portals: </b> Giúp style của component không bị ảnh hưởng bởi style của component cha mà chỉ bị ảnh hưởng bởi global style
<b>Strict Mode: </b> Chế độ nghiêm ngặt cho các phần tử con nằm trong nó
<b>Hooks: </b> Cho phép sử dụng state ngay trong functional component
<b>useState: </b> Định nghĩa state variables
<b>useEffect: </b>Quản lý vòng đời components, render khi param thứ 2 thay đổi giá trị
<b>Rules of Hooks: </b> Đừng gọi Hooks trong vòng lặp, điều kiện hoặc hàm lồng nhau
<b>ReactDOM: </b> Cập nhật DOM, nơi mà element thay đổi
<b>Synthetic event:</b> Các sự kiện như onClick, onChange, ...