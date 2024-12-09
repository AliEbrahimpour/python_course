
# مثال‌های متنوع از کتابخانه‌های پایتون

در این فایل، مجموعه‌ای از مثال‌های ساده و مفید از کتابخانه‌های مختلف پایتون آورده شده است. این مثال‌ها به شما کمک خواهند کرد تا با امکانات مختلف پایتون آشنا شوید و نحوه استفاده از آن‌ها را یاد بگیرید.

## 1. کتابخانه `math`
کتابخانه `math` شامل توابع ریاضی مختلف مانند محاسبه توان، جذر، لگاریتم و غیره است.

### مثال:
```python
import math

# محاسبه ریشه دوم
x = 16
result = math.sqrt(x)
print(f"Square root of {x} is {result}")

# محاسبه توان
power_result = math.pow(2, 3)
print(f"2 raised to the power of 3 is {power_result}")
```

## 2. کتابخانه `datetime`
کتابخانه `datetime` برای کار با تاریخ و زمان استفاده می‌شود.

### مثال:
```python
from datetime import datetime

# گرفتن زمان حال
now = datetime.now()
print("Current date and time:", now)

# فرمت‌دهی تاریخ
formatted_date = now.strftime("%Y-%m-%d %H:%M:%S")
print("Formatted date:", formatted_date)
```

## 3. کتابخانه `requests`
کتابخانه `requests` برای ارسال درخواست‌های HTTP و کار با API‌ها استفاده می‌شود.

### مثال:
```python
import requests

# ارسال درخواست GET
response = requests.get("https://api.github.com")
print("Status Code:", response.status_code)
print("Response Body:", response.json())
```

## 4. کتابخانه `pandas`
کتابخانه `pandas` برای پردازش و تحلیل داده‌ها به‌ویژه داده‌های جدولی و دیتافریم‌ها استفاده می‌شود.

### مثال:
```python
import pandas as pd

# ساخت یک دیتافریم ساده
data = {'Name': ['Alice', 'Bob', 'Charlie'], 'Age': [25, 30, 35]}
df = pd.DataFrame(data)

# نمایش دیتافریم
print(df)

# محاسبه میانگین سن‌ها
average_age = df['Age'].mean()
print(f"Average Age: {average_age}")
```

## 5. کتابخانه `matplotlib`
کتابخانه `matplotlib` برای ترسیم نمودارهای گرافیکی است.

### مثال:
```python
import matplotlib.pyplot as plt

# داده‌ها
x = [1, 2, 3, 4, 5]
y = [1, 4, 9, 16, 25]

# ترسیم نمودار خطی
plt.plot(x, y)
plt.title("Simple Plot")
plt.xlabel("X Axis")
plt.ylabel("Y Axis")
plt.show()
```

## 6. کتابخانه `numpy`
کتابخانه `numpy` برای انجام محاسبات عددی و کار با آرایه‌ها و ماتریس‌ها استفاده می‌شود.

### مثال:
```python
import numpy as np

# ایجاد یک آرایه numpy
arr = np.array([1, 2, 3, 4, 5])

# عملیات ریاضی روی آرایه
arr_squared = np.square(arr)
print("Squared array:", arr_squared)

# محاسبه مجموع آرایه
arr_sum = np.sum(arr)
print("Sum of array:", arr_sum)
```

## 7. کتابخانه `beautifulsoup4`
کتابخانه `beautifulsoup4` برای پارس کردن (تحلیل و استخراج اطلاعات از) HTML و XML استفاده می‌شود.

### مثال:
```python
from bs4 import BeautifulSoup
import requests

# دریافت صفحه وب
response = requests.get('https://example.com')
soup = BeautifulSoup(response.text, 'html.parser')

# استخراج عنوان صفحه
title = soup.title.string
print(f"Page Title: {title}")
```

## 8. کتابخانه `tensorflow`
کتابخانه `tensorflow` برای یادگیری ماشین و شبکه‌های عصبی به کار می‌رود.

### مثال:
```python
import tensorflow as tf

# ساخت یک مدل ساده
model = tf.keras.Sequential([
    tf.keras.layers.Dense(64, activation='relu', input_shape=(32,)),
    tf.keras.layers.Dense(10, activation='softmax')
])

# نمایش معماری مدل
model.summary()
```
