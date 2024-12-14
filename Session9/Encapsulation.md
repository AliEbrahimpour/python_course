
# کپسوله‌سازی (Encapsulation) در پایتون

**کپسوله‌سازی** یکی از اصول اصلی برنامه‌نویسی شیءگرا است که هدف آن مخفی کردن جزئیات پیاده‌سازی یک کلاس و محافظت از داده‌ها در برابر تغییرات غیرمجاز است. در این مفهوم، داده‌ها و متدها در یک کلاس بسته‌بندی می‌شوند و دسترسی به آن‌ها تنها از طریق رابط‌های تعریف‌شده (مانند متدها) امکان‌پذیر است.

---

## مزایای کپسوله‌سازی

1. **حفاظت از داده‌ها**: جلوگیری از تغییر مستقیم ویژگی‌ها.
2. **کاهش پیچیدگی**: مخفی کردن جزئیات پیاده‌سازی.
3. **سهولت نگهداری**: تغییرات داخلی کلاس بر سایر بخش‌های برنامه تأثیری نمی‌گذارد.

---

## نحوه پیاده‌سازی کپسوله‌سازی در پایتون

در پایتون، می‌توان از پیشوندهای زیر برای تعیین سطح دسترسی استفاده کرد:

- **عمومی (Public)**: ویژگی‌ها یا متدهایی که همه می‌توانند به آن‌ها دسترسی داشته باشند. (بدون پیشوند)
- **محافظت‌شده (Protected)**: ویژگی‌ها یا متدهایی که فقط کلاس و کلاس‌های فرزند می‌توانند به آن‌ها دسترسی داشته باشند. (پیشوند `_`)
- **خصوصی (Private)**: ویژگی‌ها یا متدهایی که فقط در داخل همان کلاس قابل دسترسی هستند. (پیشوند `__`)

---

## مثال 1: دسترسی عمومی

```python
class Person:
    def __init__(self, name, age):
        self.name = name  # عمومی
        self.age = age    # عمومی

person = Person("Ali", 25)
print(person.name)  # خروجی: Ali
print(person.age)   # خروجی: 25
```

---

## مثال 2: دسترسی محافظت‌شده

```python
class Person:
    def __init__(self, name, age):
        self._name = name  # محافظت‌شده
        self._age = age    # محافظت‌شده

    def get_details(self):
        return f"Name: {self._name}, Age: {self._age}"

person = Person("Sara", 30)
print(person.get_details())  # خروجی: Name: Sara, Age: 30
# مستقیماً می‌توان دسترسی داشت، اما پیشنهاد نمی‌شود
print(person._name)  # خروجی: Sara
```

---

## مثال 3: دسترسی خصوصی

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # خصوصی

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

    def withdraw(self, amount):
        if 0 < amount <= self.__balance:
            self.__balance -= amount

    def get_balance(self):
        return self.__balance

account = BankAccount(1000)
account.deposit(500)
print(account.get_balance())  # خروجی: 1500

account.withdraw(300)
print(account.get_balance())  # خروجی: 1200

# تلاش برای دسترسی مستقیم (خطا نمی‌دهد اما پیشنهاد نمی‌شود)
# print(account.__balance)  # AttributeError
```

---

## روش‌های دسترسی امن: متدهای Getter و Setter

برای دسترسی و تغییر مقادیر ویژگی‌های خصوصی، از متدهای **getter** و **setter** استفاده می‌شود.

```python
class Employee:
    def __init__(self, salary):
        self.__salary = salary

    # متد getter
    def get_salary(self):
        return self.__salary

    # متد setter
    def set_salary(self, value):
        if value > 0:
            self.__salary = value

employee = Employee(5000)
print(employee.get_salary())  # خروجی: 5000

employee.set_salary(6000)
print(employee.get_salary())  # خروجی: 6000
```

---

## مثال پیشرفته: پیاده‌سازی کامل کپسوله‌سازی

```python
class Car:
    def __init__(self, brand, max_speed):
        self.__brand = brand      # خصوصی
        self.__max_speed = max_speed  # خصوصی

    # Getter
    def get_brand(self):
        return self.__brand

    def get_max_speed(self):
        return self.__max_speed

    # Setter
    def set_max_speed(self, speed):
        if speed > 0:
            self.__max_speed = speed
        else:
            print("Invalid speed value!")

    def display_details(self):
        print(f"Brand: {self.__brand}, Max Speed: {self.__max_speed}")

car = Car("BMW", 240)
car.display_details()  # خروجی: Brand: BMW, Max Speed: 240

car.set_max_speed(300)
car.display_details()  # خروجی: Brand: BMW, Max Speed: 300

# تلاش برای تغییر مستقیم
# car.__brand = "Mercedes"  # AttributeError
```

---

## نکات مهم

1. **ساده‌سازی رابط کاربری**: کپسوله‌سازی داده‌ها به کاربران اجازه می‌دهد از طریق متدهای مشخص به داده‌ها دسترسی داشته باشند.
2. **محدودسازی تغییرات**: تغییرات در جزئیات داخلی بر متدهای خارجی تأثیری نمی‌گذارد.
3. **امنیت**: از تغییر غیرمجاز داده‌ها جلوگیری می‌شود.

---
