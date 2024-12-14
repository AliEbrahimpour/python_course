# وراثت (Inheritance) در پایتون

وراثت یکی از اصول برنامه‌نویسی شیءگرا است که به شما اجازه می‌دهد یک کلاس جدید ایجاد کنید که قابلیت‌ها و ویژگی‌های یک کلاس دیگر را به ارث ببرد. این مفهوم به شما کمک می‌کند تا کدهای خود را مجدداً استفاده کنید و آن‌ها را منظم‌تر کنید.

---

## تعریف پایه

وقتی کلاسی از کلاس دیگری ارث می‌برد:
- کلاس والد (Parent Class) یا پایه (Base Class): کلاسی است که ویژگی‌ها و متدها از آن ارث می‌برند.
- کلاس فرزند (Child Class) یا مشتق‌شده (Derived Class): کلاسی است که قابلیت‌ها را از کلاس والد به ارث می‌برد و می‌تواند ویژگی‌ها یا متدهای جدیدی اضافه کند.

---

## نحوه تعریف

برای استفاده از وراثت، کافی است نام کلاس والد را داخل پرانتز بعد از تعریف کلاس فرزند ذکر کنید.

```python
# تعریف کلاس والد
class Parent:
    def __init__(self, name):
        self.name = name

    def greet(self):
        print(f"Hello, I am {self.name}!")

# تعریف کلاس فرزند
class Child(Parent):
    def __init__(self, name, age):
        super().__init__(name)  # فراخوانی کانستراکتور کلاس والد
        self.age = age

    def show_age(self):
        print(f"I am {self.age} years old.")