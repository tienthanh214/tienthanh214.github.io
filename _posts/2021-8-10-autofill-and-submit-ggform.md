---
title: "Autofill and Submit Google form"
excerpt: "autofill and submit google form using requests in python"
show_date: true
tags:
  - python
categories:
  - computer science
toc: true
---

[English here](https://github.com/tienthanh214/autofill-and-submit-ggform/blob/main/README.md)

# Task
Một ngày đẹp trời, có một người nào đó đưa cho bạn một cái Google form và yêu cầu mình điền vào đó mỗi ngày, hoặc có thể và hằng giờ để báo cáo một việc gì đó.

Công việc lặp đi lặp lại này có vẻ nhàm chán, do đó mình nghĩ đến việc viết một script để làm việc này một cách tự động bằng **Python**

# Just build it
## Create and access URL
URL của Google form sẽ trông như thế này:
```
https://docs.google.com/forms/d/e/form-index/viewform
```
Copy URL đó và thay thế **viewform** bằng **formResponse**:
```
https://docs.google.com/forms/d/e/form-index/formResponse
```

## Extract information

Mở Google form cần điền lên, sau đó mở công cụ DevTools (inspect) trên web.

Mỗi input-box mà ta cần điền thông tin vào sẽ có dạng
```name = "entry.id"```. Tìm kiếm chúng với từ khóa ```entry```

![image-center](/assets/images/post/autofill-ggform-entry.png){: .align-center}

Thử điền từng input-box để biết ```id``` của nó

## Write Python script
### Fill data
Sau khi biết được ```id``` và định dạng cho từng input-box

Tạo một dictionary với ```key``` là id của từng input-box, cùng với đó là ```value``` chính là dữ liệu bạn cần nhập vào

```py
def fill_form():
    name = 'Your name'
    date, hour = str(datetime.datetime.now()).split(' ')
    date = date.split('-')
    hour = hour.split(':')

    value = {
        # Text
        "entry.648944920": name,
        # Dropdown menu
        "entry.1323047968": "Sài Gòn",
        # Date
        "entry.914980634_year": date[0],
        "entry.914980634_month": date[1],
        "entry.914980634_day": date[2],
        # Hour
        "entry.1734465153": hour[0] + 'h',
        # Checkbox 
        "entry.436161856": ["Cà phê", "Bể bơi"],
        # One choice
        "entry.1224443740": "Okay"
    }
    return value
```
**Lưu ý**: 
- Cần nhập đúng format dữ liệu có trong từng input-box nếu không sẽ không thể điền form (tốt nhất là vào form đó rồi copy dán vào code)
- Đối với checkbox multi-choice: dữ liệu sẽ dưới dạng list

## Submit form
Dùng phương thức POST của thư viện **requests**
```python
def submit(url, data):
    try:
        requests.post(url, data = data)
        print("Submitted successfully!")
    except:
        print("Error!")

submit(url, fill_form())
```
Xong!!!

Full code: [https://github.com/tienthanh214/autofill-and-submit-ggform](https://github.com/tienthanh214/autofill-and-submit-ggform)

Test yourself: [Google form - Test script](https://docs.google.com/forms/d/e/1FAIpQLSdwcwvrOeBG200L0tCSUHc1MLebycACWIi3qw0UBK31GE26Yg/viewform)

# Run it daily
Các bạn có thể sử dụng [heroku.com](https://www.heroku.com/) và dùng add-on **Heroku Scheduler** để chạy nó theo lịch cụ thể, mặc dù nó Free nhưng vẫn yêu cầu nhập credit card.

Nếu bạn không có credit card, có thể dùng [pythonanywhere.com](https://www.pythonanywhere.com/), upload code sau đó vào *Tasks*, chọn giờ chạy script vào mỗi ngày. Vì nó Free nên có rất nhiều hạn chế.



