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
  - https://sites.google.com/chromium.org/driver/
  - https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/
  - https://github.com/mozilla/geckodriver/releases
  - https://webkit.org/blog/6900/webdriver-support-in-safari-10/

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

### Điền vào Form

Có thể mô phỏng việc click chọn vào Option HTML tags bằng selenium

```python
element = driver.find_element(By.XPATH, "//select[@name='name']")
all_options = element.find_elements(By.TAG_NAME, "option")
for option in all_options:
    print("Value is: %s" % option.get_attribute("value"))
    option.click()
```

Có thể tùy chọn select các thẻ:

```python
from selenium.webdriver.support.ui import Select
select = Select(driver.find_element(By.NAME, 'name'))
select.select_by_index(index) # Chọn với index
select.select_by_visible_text("text") # Chọn với text
select.select_by_value(value) # Chọn với giá trị
```

Hoặc bỏ chọn tất cả:
```python
select = Select(driver.find_element(By.ID, 'id'))
select.deselect_all()
```

Lấy danh sách các thẻ được chọn mặc định:
```python
select = Select(driver.find_element(By.XPATH, "//select[@name='name']"))
all_selected_options = select.all_selected_options
```

Submit với nút
```python
# Assume the button has the ID "submit" :)
driver.find_element_by_id("submit").click()
```

Ngoài ra, nếu bạn gọi Element đó trong 1 form, selenium sẽ cố gắng tìm cách submit nó:
```python
element.submit()
```

### Kéo và thả

Bạn có thể sử dụng kéo và thả, di chuyển một phần tử theo một số lượng nhất định hoặc chuyển sang một phần tử khác:

```python
element = driver.find_element(By.NAME, "source")
target = driver.find_element(By.NAME, "target")

from selenium.webdriver import ActionChains
action_chains = ActionChains(driver)
action_chains.drag_and_drop(element, target).perform()
```

```python
driver.switch_to_window("windowName")

for handle in driver.window_handles:
    driver.switch_to_window(handle)

driver.switch_to_frame("frameName")

driver.switch_to_frame("frameName.0.child")

driver.switch_to.default_content()
```

### Popup dialogs

Selenium có thể xử lý các hộp thoại bật lên. Chấp nhận, loại bỏ, đọc nội dung hoặc thậm chí nhập vào một lời nhắc.

```python
alert = driver.switch_to.alert
```

### Navigation: History
```python
driver.forward()
driver.back()
```
### Cookies

```python
# Go to the correct domain
driver.get("http://www.example.com")

# Now set the cookie. This one's valid for the entire domain
cookie = {‘name’ : ‘foo’, ‘value’ : ‘bar’}
driver.add_cookie(cookie)

# And now output all the available cookies for the current URL
driver.get_cookies()
```


