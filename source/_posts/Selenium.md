---
title: Selenium
date: 2022-10-11 14:35:39
tags: [python, selenium]
---

## Cài đặt

- Cài đặt thư viện Selenium:
```bash
python -m pip install selenium
# Hoặc
pip install selenium
```
- Cài đặt driver theo tùy trình duyệt và add vào PATH:
    * https://sites.google.com/chromium.org/driver/
    * https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/
    * https://github.com/mozilla/geckodriver/releases
    * https://webkit.org/blog/6900/webdriver-support-in-safari-10/

## Sử dụng

### Simple Usage

Chạy chương trình này để chắc chắn rằng Selenium và Driver của bạn đã được cài đặt:

```python
from selenium import webdriver

from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()
driver.get("http://www.python.org")
assert "Python" in driver.title
elem = driver.find_element(By.NAME, "q")
elem.clear()
elem.send_keys("pycon")
elem.send_keys(Keys.RETURN)
assert "No results found." not in driver.page_source
driver.close()
```

### Navigating

Mở trình duyệt
```python
driver.get("http://huytm2k3.github.io")
```

### Interacting

Để tìm 1 phần tử HTML như sau:
```html
<input type="text" name="passwd" id="passwd-id" />
```
Chúng ta có 4 cách:

```python
element = driver.find_element(By.ID, "passwd-id")
element = driver.find_element(By.NAME, "passwd")
element = driver.find_element(By.XPATH, "//input[@id='passwd-id']")
element = driver.find_element(By.CSS_SELECTOR, "input#passwd-id")
```

![](/images/SeleniumPost/Screenshot_1.png)

Có thể mô phỏng nút bấm, nhập văn bản bằng phương thức send_keys:

```python
element.send_keys("some text")
element.send_keys(" and some", Keys.ARROW_DOWN)
```
