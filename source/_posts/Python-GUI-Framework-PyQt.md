---
title: Python GUI Framework PyQt
date: 2022-12-07 14:55:17
tags:
---

## PyQt là gì?

PyQt là một liên kết Python của bộ công cụ GUI đa nền tảng Qt, được triển khai dưới dạng một trình cắm thêm Python. PyQt là phần mềm miễn phí được phát triển bởi công ty Riverbank Computing của Anh.

## Cấu trúc cơ bản

```py
from PyQt6.QtWidgets import QApplication, QWidget
import sys
from PyQt6.QtGui import QIcon

class Window(QWidget):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("PyQt6 Window")
        # ... Define window here!


app = QApplication([])
window = Window()
window.show()
sys.exit(app.exec())
```

## Thuộc tính cơ bản QWidget

```py
self.setWindowTilte("Title here!") # Sửa tiêu đề cửa sổ
self.setWindowIcon(...) # Sửa icon
self.setFixedHeight(200) # Chiều cao cửa sổ
self.setFixedWidth(200) # Chiều rộng cửa sổ
self.setGeometry(a,b,c,d) # Vị trí khởi động của cửa sổ và width height
self.setStyleSheet(...) # CSS cho cửa sổ
```

## Load \*.ui file

```py
from PyQt6.QtWidgets import QApplication, QWidget
from PyQt6 import uic
import sys

class UI(QWidget):
    def __init__(self):
        super().__init__()
        uic.loadUi('./ui/main.ui', self)

app = QApplication(sys.argv)
window = UI()
window.show()
sys.exit(app.exec())
```

## Convert ui file thành py file

```bash
pyuic6 -x <uifile> -o <pyfile>
```

## PushButton and Label

```py
from PyQt6.QtWidgets import QApplication, QWidget, QPushButton, QLabel
import sys
from PyQt6.QtGui import QIcon, QFont

class Window(QWidget):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("PyQt6 Window")
        
        self.setGeometry(500, 200, 500, 400)

        self.create_widgets()

    def create_widgets(self):
        btn = QPushButton("Click Me", self)
        # btn.move(100, 100)
        btn.setGeometry(100, 100, 100, 100)
        btn.setStyleSheet('background-color: red')
        # Click event 
        btn.clicked.connect(self.clicked_btn)

        self.label = QLabel("My Label", self)
        self.label.move(100, 200)
        self.label.setStyleSheet('color: green')
        self.label.setFont(QFont("Times New Roman", 15))

    # Set text for label
    def clicked_btn(self):
        self.label.setText("Clicked!")


app = QApplication([])
window = Window()
window.show()
sys.exit(app.exec())
```

