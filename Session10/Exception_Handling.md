
# مدیریت خطا در شیءگرایی (Exception Handling in Object-Oriented Programming)

مدیریت خطا یکی از مفاهیم کلیدی در توسعه نرم‌افزار است که به ما کمک می‌کند خطاها را شناسایی، دسته‌بندی و به درستی مدیریت کنیم. در برنامه‌نویسی شیءگرا، مدیریت خطا اغلب از طریق **استثناها (Exceptions)** انجام می‌شود.

---

## اصول مدیریت خطا در شیءگرایی

1. **تشخیص خطا**: شناسایی شرایطی که ممکن است باعث خرابی برنامه شوند.
2. **گزارش خطا**: اعلام وقوع خطا از طریق پرتاب استثنا (throwing exceptions).
3. **مدیریت خطا**: نوشتن کد برای پاسخ به خطا و جلوگیری از توقف برنامه.
4. **تمیزکاری منابع**: اطمینان از آزادسازی منابع (مثل فایل‌ها یا کانکشن‌ها) حتی در صورت وقوع خطا.

---

## مراحل مدیریت خطا در پایتون

### 1. استفاده از بلوک `try-except`
برای کنترل استثناها، کدی که ممکن است خطا ایجاد کند در بلوک `try` قرار می‌گیرد و مدیریت خطا در بلوک `except` انجام می‌شود.

```python
try:
    number = int(input("Enter a number: "))
    print(f"You entered: {number}")
except ValueError:
    print("Invalid input! Please enter a valid number.")
```

---

### 2. بلوک‌های `finally` و `else`

- **`finally`**: همیشه اجرا می‌شود، چه خطایی رخ دهد چه ندهد.
- **`else`**: اجرا می‌شود فقط اگر خطایی رخ نداده باشد.

```python
try:
    file = open("example.txt", "r")
    content = file.read()
except FileNotFoundError:
    print("File not found!")
else:
    print(content)
finally:
    if 'file' in locals() and not file.closed:
        file.close()
```

---

### 3. تعریف استثنای سفارشی

می‌توانید کلاس‌های استثنا سفارشی تعریف کنید تا خطاهای خاصی را مدیریت کنید.

```python
class CustomError(Exception):
    def __init__(self, message):
        super().__init__(message)

def divide(a, b):
    if b == 0:
        raise CustomError("Division by zero is not allowed!")
    return a / b

try:
    result = divide(10, 0)
except CustomError as e:
    print(f"Custom Error: {e}")
```

---

## انواع مختلف خطاها در پایتون

1. **خطاهای استاندارد (Built-in Exceptions)**: مانند `ValueError`, `TypeError`, `IndexError`.
2. **خطاهای منطقی (Logical Errors)**: خطاهایی که در کد وجود دارند اما باعث ایجاد استثنا نمی‌شوند (مانند محاسبات اشتباه).
3. **استثناهای سفارشی (Custom Exceptions)**: تعریف‌شده توسط توسعه‌دهنده.

---

## مثال‌های متنوع از مدیریت خطا

### مثال 1: مدیریت چندین نوع استثنا

```python
try:
    num = int(input("Enter a number: "))
    result = 10 / num
except ValueError:
    print("Invalid input! Please enter a number.")
except ZeroDivisionError:
    print("Cannot divide by zero!")
else:
    print(f"Result: {result}")
finally:
    print("Execution complete.")
```

---

### مثال 2: استفاده از استثنای سفارشی برای محدودیت‌های منطقی

```python
class AgeError(Exception):
    pass

def check_age(age):
    if age < 18:
        raise AgeError("Age must be at least 18.")

try:
    age = int(input("Enter your age: "))
    check_age(age)
except AgeError as e:
    print(f"Error: {e}")
```

---

### مثال 3: جمع‌آوری اطلاعات خطا با ماژول `logging`

برای ثبت خطاها در یک فایل یا کنسول می‌توان از ماژول `logging` استفاده کرد.

```python
import logging

logging.basicConfig(filename="app.log", level=logging.ERROR)

try:
    result = 10 / 0
except ZeroDivisionError as e:
    logging.error(f"Error occurred: {e}")
```

---

### مثال 4: مدیریت خطا در کلاس‌ها

```python
class BankAccount:
    def __init__(self, balance):
        self.balance = balance

    def withdraw(self, amount):
        if amount > self.balance:
            raise ValueError("Insufficient funds!")
        self.balance -= amount
        return self.balance

try:
    account = BankAccount(1000)
    print(account.withdraw(1500))
except ValueError as e:
    print(f"Transaction failed: {e}")
```

---

### مثال 5: مدیریت زنجیره‌ای خطاها

در مواقعی که یک خطا باید به صورت زنجیره‌ای مدیریت شود.

```python
def open_file(filename):
    try:
        with open(filename, "r") as file:
            return file.read()
    except FileNotFoundError as e:
        raise RuntimeError("Failed to read file") from e

try:
    content = open_file("nonexistent.txt")
except RuntimeError as e:
    print(f"Error: {e}")
```

---

## نکات مهم

1. **استفاده از `try-except` برای سناریوهای خاص**: از بلوک‌های مدیریت خطا فقط برای کدی استفاده کنید که احتمال وقوع خطا در آن زیاد است.
2. **اجتناب از مدیریت خطای عمومی**: از یک بلوک عمومی مانند `except Exception` فقط در شرایط خاص استفاده کنید.
3. **تمیزکاری منابع**: همیشه از بلوک `finally` یا مدیریت زمینه (Context Manager) برای آزادسازی منابع استفاده کنید.
4. **ثبت خطاها**: خطاها را برای تحلیل و رفع مشکلات ثبت کنید.

---

