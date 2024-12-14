
# الگوهای طراحی شی‌گرا (Object-Oriented Design Patterns)

الگوهای طراحی شی‌گرا راه‌حل‌های عمومی و قابل استفاده مجدد برای مشکلات رایج در طراحی نرم‌افزار هستند. این الگوها به توسعه‌دهندگان کمک می‌کنند کدهای تمیز، قابل فهم و قابل نگهداری بنویسند.

الگوهای طراحی به سه دسته اصلی تقسیم می‌شوند:
1. **الگوهای خلاقانه (Creational Patterns)**: مدیریت نحوه ایجاد اشیا.
2. **الگوهای ساختاری (Structural Patterns)**: ساختار و رابطه بین اشیا.
3. **الگوهای رفتاری (Behavioral Patterns)**: تعامل و مسئولیت بین اشیا.

---

## 1. الگوهای خلاقانه (Creational Patterns)

### 1.1 Singleton Pattern
**هدف**: اطمینان حاصل می‌کند که یک کلاس تنها یک نمونه (Instance) دارد و دسترسی سراسری به آن را فراهم می‌کند.

**مثال در پایتون**:
```python
class Singleton:
    _instance = None

    def __new__(cls, *args, **kwargs):
        if not cls._instance:
            cls._instance = super(Singleton, cls).__new__(cls)
        return cls._instance

s1 = Singleton()
s2 = Singleton()
print(s1 is s2)  # True
```

---

### 1.2 Factory Method
**هدف**: یک رابط برای ایجاد اشیا فراهم می‌کند اما اجازه می‌دهد زیرکلاس‌ها نوع اشیایی که ایجاد می‌شوند را تعیین کنند.

**مثال**:
```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

class AnimalFactory:
    @staticmethod
    def create_animal(animal_type):
        if animal_type == "dog":
            return Dog()
        elif animal_type == "cat":
            return Cat()
        else:
            raise ValueError("Unknown animal type")

animal = AnimalFactory.create_animal("dog")
print(animal.speak())  # Woof!
```

---

### 1.3 Builder Pattern
**هدف**: فرآیند ساخت یک شیء پیچیده را به گام‌های ساده تقسیم می‌کند.

**مثال**:
```python
class BurgerBuilder:
    def __init__(self):
        self.ingredients = []

    def add_patty(self):
        self.ingredients.append("Patty")
        return self

    def add_lettuce(self):
        self.ingredients.append("Lettuce")
        return self

    def add_cheese(self):
        self.ingredients.append("Cheese")
        return self

    def build(self):
        return "Burger with " + ", ".join(self.ingredients)

burger = BurgerBuilder().add_patty().add_cheese().add_lettuce().build()
print(burger)  # Burger with Patty, Cheese, Lettuce
```

---

## 2. الگوهای ساختاری (Structural Patterns)

### 2.1 Adapter Pattern
**هدف**: رابط یک کلاس را برای کلاس‌های دیگر که رابط‌های مختلفی دارند سازگار می‌کند.

**مثال**:
```python
class EuropeanSocket:
    def voltage(self):
        return "220V"

class USASocket:
    def voltage(self):
        return "110V"

class SocketAdapter:
    def __init__(self, socket):
        self.socket = socket

    def voltage(self):
        return self.socket.voltage()

adapter = SocketAdapter(EuropeanSocket())
print(adapter.voltage())  # 220V
```

---

### 2.2 Decorator Pattern
**هدف**: به صورت پویا رفتار یک شیء را اضافه می‌کند.

**مثال**:
```python
class Coffee:
    def cost(self):
        return 5

    def description(self):
        return "Plain Coffee"

class MilkDecorator:
    def __init__(self, coffee):
        self._coffee = coffee

    def cost(self):
        return self._coffee.cost() + 2

    def description(self):
        return self._coffee.description() + ", Milk"

coffee = Coffee()
coffee_with_milk = MilkDecorator(coffee)
print(coffee_with_milk.description())  # Plain Coffee, Milk
print(coffee_with_milk.cost())  # 7
```

---

## 3. الگوهای رفتاری (Behavioral Patterns)

### 3.1 Strategy Pattern
**هدف**: خانواده‌ای از الگوریتم‌ها را تعریف کرده و استفاده از آن‌ها را پویا انتخاب می‌کند.

**مثال**:
```python
class Strategy:
    def execute(self, a, b):
        pass

class Add(Strategy):
    def execute(self, a, b):
        return a + b

class Multiply(Strategy):
    def execute(self, a, b):
        return a * b

class Context:
    def __init__(self, strategy):
        self.strategy = strategy

    def execute_strategy(self, a, b):
        return self.strategy.execute(a, b)

context = Context(Add())
print(context.execute_strategy(3, 4))  # 7

context = Context(Multiply())
print(context.execute_strategy(3, 4))  # 12
```

---

### 3.2 Observer Pattern
**هدف**: به اشیاء مختلف اجازه می‌دهد که از تغییر وضعیت یک شیء خاص آگاه شوند.

**مثال**:
```python
class Subject:
    def __init__(self):
        self._observers = []

    def attach(self, observer):
        self._observers.append(observer)

    def notify(self):
        for observer in self._observers:
            observer.update()

class Observer:
    def update(self):
        pass

class ConcreteObserver(Observer):
    def update(self):
        print("Observer has been notified!")

subject = Subject()
observer = ConcreteObserver()

subject.attach(observer)
subject.notify()  # Observer has been notified!
```

---

## منابع برای یادگیری بیشتر
- **کتاب‌ها**: 
  - *Design Patterns: Elements of Reusable Object-Oriented Software* توسط Gang of Four (GoF)
  - *Head First Design Patterns*
- **دوره‌های آنلاین**:
  - Coursera، Udemy و Pluralsight
- **سایت‌ها**:
  - [Refactoring Guru](https://refactoring.guru/)
  - [Geeks for Geeks](https://www.geeksforgeeks.org/)
```

