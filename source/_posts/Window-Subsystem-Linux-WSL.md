---
title: Window Subsystem Linux (WSL)
date: 2022-04-23 15:59:35
tags: [windows,wsl,ubuntu,linux]
categories: [Other]
---
## Giới thiệu

Source: 
https://xuanthulab.net/gioi-thieu-va-cai-dat-wsl-tren-windows.html
https://docs.microsoft.com/en-us/windows/wsl/install-manual

Mọi thắc mắc xin liên hệ tới:
- Facebook: https://www.facebook.com/profile.php?id=100072417355186 (Tạ Minh Huy)
- Zalo: 0522566897
- Email: Huyat180522@gmail.com

WSL (Windows Subsystem for Linux) là một tính năng có trên Windows x64 (từ Windows 10, bản 1607 và trên Windows Server 2019), nó cho phép chạy hệ điều hành Linux (GNU/Linux) trên Windows. Với WSL bạn có thể chạy các lệnh, các ứng dụng trực tiếp từ dòng lệnh Windows mà không phải bận tâm về việc tạo / quản lý máy ảo như trước đây.

Dễ hiểu thì là chạy Terminal của Linux trên Windows. Bài viết này được mình sưu tầm và viết lại một cách ngắn gọn, dễ hiểu nhất.

## Installation

Điều kiện:
- Máy đã bật chế độ ảo hóa của CPU (CPU Virtualization)
- Windows 10 (64 bit, version 1607) trở đi hoặc Windows Server 2019

Cách kiểm tra phiên bản Windows:

```PowerShell
[System.Environment]::OSVersion.Version
```

### Cài đặt
Mở PowerShell(PS) với quyền Administrator
```PowerShell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
```PowerShell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all
```
Sau khi nó kích hoạt, nhấn Y trả lời câu hỏi như hình trên để khởi động lại máy. Khởi động lại máy, vào dòng lệnh gõ lệnh kiểm tra danh dách các distro (bản linux) đã được cài đặt:
![](/images/WslPost/Screenshot_1.png)
```PowerShell
wsl -l --all
```
![](/images/WslPost/Screenshot_2.png)

Tải app "Ubuntu" trên MS Stores và mở.
![](/images/WslPost/Screenshot_3.png)

Thiết lập username và password cho Linux:
![](/images/WslPost/Screenshot_4.png)