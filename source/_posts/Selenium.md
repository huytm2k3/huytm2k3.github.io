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
### Locating

```python
find_element(By.ID, "id")
find_element(By.NAME, "name")
find_element(By.XPATH, "xpath")
find_element(By.LINK_TEXT, "link text")
find_element(By.PARTIAL_LINK_TEXT, "partial link text")
find_element(By.TAG_NAME, "tag name")
find_element(By.CLASS_NAME, "class name")
find_element(By.CSS_SELECTOR, "css selector")
```

### Wait

Ngày nay, phần nhiều website sử dụng AJAX, tức là khi tải trang web, một số phần tử chưa được tải ngay (Chưa có trong DOM), nên việc định vị là rất khó khăn. Vì vậy Selenium có Wait.

#### Chờ đợi rõ ràng (Explicit Waits)

```py
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Firefox()
driver.get("http://somedomain/url_that_delays_loading")
try:
    element = WebDriverWait(driver, 10).until(
        EC.presence_of_element_located((By.ID, "myDynamicElement"))
    )
finally:
    driver.quit()
```

Điều kiện:
- title_is
- title_contains
- presence_of_element_located
- visibility_of_element_located
- visibility_of
- presence_of_all_elements_located
- text_to_be_present_in_element
- text_to_be_present_in_element_value
- frame_to_be_available_and_switch_to_it
- invisibility_of_element_located
- element_to_be_clickable
- staleness_of
- element_to_be_selected
- element_located_to_be_selected
- element_selection_state_to_be
- element_located_selection_state_to_be
- alert_is_present

```python
from selenium.webdriver.support import expected_conditions as EC

wait = WebDriverWait(driver, 10)
element = wait.until(EC.element_to_be_clickable((By.ID, 'someid')))
```

Tùy chỉnh điều kiện:
```python
class element_has_css_class(object):
  """An expectation for checking that an element has a particular css class.

  locator - used to find the element
  returns the WebElement once it has the particular css class
  """
  def __init__(self, locator, css_class):
    self.locator = locator
    self.css_class = css_class

  def __call__(self, driver):
    element = driver.find_element(*self.locator)   # Finding the referenced element
    if self.css_class in element.get_attribute("class"):
        return element
    else:
        return False

# Wait until an element with id='myNewInput' has class 'myCSSClass'
wait = WebDriverWait(driver, 10)
element = wait.until(element_has_css_class((By.ID, 'myNewInput'), "myCSSClass"))
```

#### Chờ đợi ngầm (Implicit Waits)

```python
from selenium import webdriver

driver = webdriver.Firefox()
driver.implicitly_wait(10) # seconds
driver.get("http://somedomain/url_that_delays_loading")
myDynamicElement = driver.find_element_by_id("myDynamicElement")
```

Chi tiết hơn: https://selenium-python.readthedocs.io/

