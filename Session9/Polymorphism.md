
# چندریختی (Polymorphism) در پایتون

**چندریختی (Polymorphism)** یکی از اصول اصلی برنامه‌نویسی شیءگرا است که به معنای "چند شکلی" است. این مفهوم به شما اجازه می‌دهد که یک متد، کلاس یا عملگر، رفتارهای مختلفی بر اساس نوع داده‌ای که با آن کار می‌کند، داشته باشد.

---

## مزایای چندریختی

1. **انعطاف‌پذیری کد**: امکان استفاده از یک متد یا کلاس برای انواع مختلف داده‌ها.
2. **کاهش تکرار کد**: نیازی به تعریف متدهای جداگانه برای هر نوع داده نیست.
3. **سازگاری با اصل طراحی باز-بسته (Open-Closed Principle)**: می‌توانید کد را بدون تغییر بخش‌های موجود گسترش دهید.

---

## انواع چندریختی در پایتون

1. **چندریختی در متدها**: یک متد با نام مشابه می‌تواند رفتار متفاوتی در کلاس‌های مختلف داشته باشد.
2. **چندریختی در عملگرها**: یک عملگر مانند `+` می‌تواند برای انواع مختلفی از داده‌ها رفتار متفاوتی داشته باشد.

---

## مثال 1: چندریختی در متدها (Method Overriding)

وقتی یک کلاس فرزند، متدی با همان نام متد کلاس والد بازنویسی می‌کند، رفتار متد تغییر می‌کند.

```python
class Animal:
    def speak(self):
        print("The animal makes a sound")

class Dog(Animal):
    def speak(self):
        print("The dog barks")

class Cat(Animal):
    def speak(self):
        print("The cat meows")

# استفاده
animals = [Dog(), Cat(), Animal()]
for animal in animals:
    animal.speak()
```

**خروجی:**
```
The dog barks
The cat meows
The animal makes a sound
```

---

## مثال 2: چندریختی با متدهای مشابه

می‌توانید متدهایی با نام مشابه در کلاس‌های مختلف تعریف کنید که رفتار متفاوتی داشته باشند.

```python
class Rectangle:
    def area(self, length, width):
        return length * width

class Circle:
    def area(self, radius):
        return 3.14 * radius * radius

shapes = [Rectangle(), Circle()]

# استفاده از متدها
print(shapes[0].area(10, 5))  # خروجی: 50
print(shapes[1].area(7))      # خروجی: 153.86
```

---

## مثال 3: چندریختی در عملگرها (Operator Overloading)

عملگرها در پایتون می‌توانند برای کلاس‌های مختلف بازتعریف شوند. این فرآیند به **عملگر سربارگذاری (Operator Overloading)** معروف است.

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)

    def __str__(self):
        return f"({self.x}, {self.y})"

point1 = Point(2, 3)
point2 = Point(4, 5)

result = point1 + point2
print(result)  # خروجی: (6, 8)
```

---

## چندریختی با توابع داخلی

در پایتون، توابع داخلی مانند `len()` رفتار متفاوتی با انواع داده‌های مختلف دارند.

```python
print(len("Hello"))  # خروجی: 5 (طول رشته)
print(len([1, 2, 3]))  # خروجی: 3 (تعداد عناصر لیست)
```

---

## مزیت چندریختی در برنامه‌نویسی شیءگرا

1. افزایش **انعطاف‌پذیری** کد.
2. تسهیل **افزودن قابلیت‌های جدید**.
3. **کاهش وابستگی** بین اجزای مختلف کد.

---

