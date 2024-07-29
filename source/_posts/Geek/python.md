---
title: Python
tags: python
categories: Geek
abbrlink: a378bd8e
date: 2024-03-03 20:24:00
---

# 面向对象概念与设计原则
## 面向对象编程的基本原理
### 类与对象
程序是由多种对象组合而成。
类是对象的类型定义，每一个对象都有类型，每一种类型的对象，都有同样的属性和方法。
对象是具备属性和功能的实例，而类则是定义属性和功能的模板。
类和对象的关系：类是对象的抽象，对象是类的实例。
### 封装
定义一个类的过程就是将一些相关的属性和方法组织在一起的过程。这样的操作被称为封装。
### 继承
子类继承父类，那么子类就拥有了父类的的所有属性和方法。
使用继承的方式复用类定义的代码
### 多态
由一个类实例化出来的对象之间是相互独立的，不同对象虽然具备相同作用的属性和方法。但是由于它们各自在程序中扮演的角色不同，相同的属性值也将各自不同，相同的方法运行的结果也会不同。
这种同类对象各自独立的特性也被称为多态。
## 面向对象设计
### 接口与抽象类
接口是一种对程序模块间互相访问方式的约定，在面向对象语言中，一般都会使用抽象类来定义。
抽象类指的是一种只定义了行为，但并没有提供完整功能实现的类。
举例：交通工具这样一个概念就可以被理解为一个抽象类或者一个接口。它只定义了交通工具运输的功能，但是并没有限制实现的方法。无论是汽车还是轮船，只要提供了对应的功能。就都符合了交通工具这个类型的定义。
### 面向接口的设计模式
面向接口指的是以面向对象的方式定义程序功能和模块间传递数据的格式，以面向接口的方式设计程序框架结构是建立复杂程序的基础。
举例：在图形界面编程中定义一个按钮，我们会考虑到按钮需要可以被点击，点击可以触发一个信号来做一些别的事情，这就是一个行为，我们可以定义一个方法来描述这个行为。而这个按钮上，还有它的外观，比如形状尺寸等，按钮上面的文字，图标，控件的名称等等这些信息，有的是数字有的是文字有的是其他类型的对象。因此作为一个按钮对象，除了提供行为能力的方法之外，还需要各种类型的属性来支持。而设计一个界面编程库的时候，我们显然并不需要立刻就实例化一个真正的按钮控件，此时需要做的就是定义将来真正的按钮控件，被实例化时应当符合的规则。在设计接口时，我们需要做的就是创建一个类型来定义这些信息,并提示开发者在使用这个库的时候，完成这些抽象定义的具体实现，面向接口的设计模式从架构层面出发，从开发之初就预先定义了程序的复杂度，在之后的开发工作中，编程工作只需要不断地细化程序功能的实现从而避免随着开发的继续程序复杂度无限制的膨胀的问题。
## SOLID原则
设计模式的五大基本原则根据英文被统称为SOLID原则：
![alt text](image.png)
### 单一职责原则
单一职责原则指的是一个模块或一个类应当只承担一个职责，如果一个类在程序中同时扮演多种角色的话，当其中一个功能面临修改时势必会影响其他功能的使用。
在程序开发的阶段，一个类被修改的几率是很大的，因此应该专注于单一的功能。
### 开放封闭原则
开放封闭原则指的是对扩展开放，对修改封闭，调整已存在的代码逻辑，往往会破坏与之相关的诸多模块。而在相同的逻辑规则下，增加更多的不同功能的插件实现，则可以有效的保持程序的稳定性。
如果提前划分了模块，并定义了各种模块的程序接口，当遇到需要调整某个模块才能适应新需求的问题时，只需要实现新的符合程序接口的模块即可实现适配。这样一个需要修改的问题就变成了扩展问题了。
实现更多变种的模块，以适应更多的需求实际上只是对程序的扩展，而非牵扯内部逻辑关系的修改，支持扩展反对修改就是开放封闭原则的关键。
### 里氏替换原则
里氏替换原则规定子类或以任何形式派生的类，都应当具备完全替代父类的能力。这意味着在编程中，当我们需要依赖一个明确定义的接口类型时，可以放心地依赖这个类，以及其任意子类实例地对象。而无需担心程序地预期行为受到影响。
举例：假如定义了一个交通工具这个父类，并实现了一个行驶的方法，假设这个方法允许输入一个目的地类型的对象从而改变当前对象的位置。如果继承交通工具来创建一个叫做汽车的子类，无论我们如何扩展这个子类，必须保证的是，他依然具备父类的功能，也就是行驶的方法，其输入的参数类型以及作用应当与父类保持一致。
通俗地讲：子类对象必须是一种更为具体地父类对象，一辆汽车必须是一个交通工具，否则它就不符合里氏替换原则，这样才能确保已经依赖了交通工具类型对象的模块，再将对象替换为汽车时依然是有效的。一个可以操作maya节点的程序，必须可以操作maya中的多边形节点，因为多边形节点必须与maya节点具备符合里氏替换的原则的关系。
### 接口隔离原则
接口，是模块行为的描述。在程序构建阶段，我们需要定义的类型，都需要继承并实现接口中定义的功能。因此接口应当尽可能的单纯。换句话说，类不应该被迫地依赖它们不使用的方法。在python中语言本身并没有提供标准的接口类型，因此执行接口隔离原则需要具备对面向对象设计中的各种抽象概念有较深入的认识。
### 依赖倒置原则
依赖倒置原则主张在程序开发中，当模块之间互相关联时，应当依赖抽象而不应当依赖具体。假如实现一个控制多功能的渲染农场的程序，这个程序需要支持多种格式的任务文件。如果在开发中并没有提前定义一个任务文件的接口类型，而是直接在程序中依赖一些具体的文件格式，当需要支持新的格式时，势必无法避免重构所涉及这些对象的代码，这样的设计无疑造成了开发工作量和维护难度的增加。
# 闭包
定义了一个函数,这个函数里有个内部函数,这个内部函数使用了函数中定义的变量,当外部函数执行完毕后,内部函数依然可以访问和操作外部函数中的变量.

```python
def greeting():
    message = "hello"
    value = 20

    def inner():
        print(f'{value} - {message}')

    message = "second"

    return inner


f = greeting()
print(f.__closure__) 
f()
```
# python自带的装饰器
在定义函数时可以使用装饰器来改变函数的性质。
```python
from functools import wraps


# def welcome(fn):
#     @wraps(fn)
#     def wrapper(*args, **kwargs):
#         print("Welcome")
#         result = fn(*args, **kwargs)
#         return result
#
#     return wrapper

def welcome(name):
    def decorator(fn):
        @wraps(fn)
        def wrapper(*args, **kwargs):
            print(f"Welcome {name}")
            result = fn(*args, **kwargs)
            return result

        return wrapper
    return decorator


@welcome("Tom")
def my_fun(message: str):
    print(f"Hello {message}")


@welcome("Mary")
def my_fun_2():
    print("my fun 2")


# f1 = welcome(my_fun)
# f1("Jack")

my_fun("Jack")

print(my_fun.__name__)
```
## property
property是一个用于创建特殊属性的装饰器，他的功能是将一个方法转换为一个属性，方法的返回值就是属性的返回值。
使用property装饰器定义的属性具有只读的特性，他的值在每一次被访问时，是实时的被计算出来的。
一般来说我们调用类的方法都是加一个括号，但是如果这个方法添加了property装饰器，那么我们就可以像调用类的属性一样直接使用这个方法调用返回的结果。
## attr.setter
这里的attr是经过property装饰后的方法的名字。因为经过property装饰后的方法就变成只能读的属性了，要想通过对象修改这个属性就需要使用setter装饰器
## classmethod
类中定义的不加装饰器的方法都是实例方法，都需要一个self参数，而用classmethod装饰器装饰的方法被称为类方法，它需要的第一个参数不是self而是cls参数，用于表示类本身，类方法只能被类直接的调用，而不能在对象下调用。 
## staticmethod
被staticmethod装饰的方法叫静态方法，静态方法不需要传入self或cls参数。
静态方法和定义在类以外的方法是相似的。
# 类与装饰器
可以通过类来定义函数装饰器,也可以给类定义装饰器.
```python
# 以下装饰器实现的功能是在原来功能的基础上添加输出start与输出end的功能

# 创建一个不需要参数的通过类定义的函数装饰器
class MyDecorator:
    def __init__(self, f):
        self.f = f

    def __call__(self, *args, **kwargs):
        print("start")
        result = self.f(*args, **kwargs)
        print("end")
        return result

# 创建一个带参数的通过类定义的函数装饰器
class ParamDecorator:
    def __init__(self, name):
        self.name = name

    def __call__(self, f):
        def wrap(*args):
            print(f"start {self.name}")
            result = f(*args)
            print("end")
            return result

        return wrap


@ParamDecorator("Jack")
def test():
    print("test")
    return 200


print(test())

# 定义类的装饰器
def cls_decorator(cls):
    print("start class decorator")

    def inner():
        print("start")
        obj = cls()
        print("end")
        return obj

    return inner


@cls_decorator
class Person:
    pass

p1 = Person()
p2 = Person()
```
# 迭代器
> 迭代器（Iterator）是访问集合元素的一种方式。在Python中，迭代器对象必须实现两个特殊方法，  \__iter\__()   和   \__next\__()  。
>   \__iter\__()  : 返回迭代器对象本身。如果类定义了此方法，则可以使用 in 语句和 for 循环来遍历。 
>   \__next\__()  : 返回下一个值。如果没有后续元素，应该抛出StopIteration 异常。
```python
class Square:
    def __init__(self,count):
        self.count = count
        self.current = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        result = self.current**2
        self.current += 1

        if self.current > self.count:
            raise StopIteration
        return result
Square_obj = Square(5)
for i in Square_obj:
    print(i)
```

# 生成器
当一个函数里包含yield语句时,这个函数就是一个生成器,生成器用来生成东西,相比return语句有个本质的区别:return在函数中只能返回一次,yield可以返回很多次.
这个函数执行后返回一个生成器对象,这个对象是可以迭代的.
生成器的好处是更节省内存,只要在用到数据的时候才会加载数据到内存中.
next(生成器对象)可以用来迭代
```python
def hello():  # an iteratable object
    print("step 1")
    yield 1
    print("step 2")
    yield 2
    print("step 3")
    yield 3


def my_fun():
    result = []
    for n in range(3):
        result.append(n ** 2)

    return result


g = hello()
for res in g:
    print(res)

# 通过生成器来实现上一章的迭代器实现的功能也可以实现这里my_fun的功能
def squares(count: int):
    for n in range(count):
        yield n ** 2


for num in squares(3):
    print(num)
```

# 上下文管理器
上下管理器是一个对象,它定义了运行时的上下文,上下文管理器为它造出来的对象定义了一个时间段,在这个时间段开始的时候做一件事情,在结束的时候做另外一件事情,在时间段开始到结束之间可以使用这个上下文管理器对象.
上下文管理器的类需要实现以下方法:
\__enter\__():上下文管理器造出来时执行,并且enter返回的对象为上下文管理器的别名
\__exit\__(): 上下文管理器结束后执行的内容
```python
# instance = open("mydata.txt", "w")
# instance.write("Hello this is a test file")
# instance.close()

# with open("mydata.txt", "w") as instance:
#     instance.write("Hello this is a test file")
#
#
# print("The end")
import time

# 定义实现上下文管理器的类
class Timer:
    def __init__(self):
        self.elapsed = 0

    def __enter__(self):
        self.start = time.perf_counter()
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self.stop = time.perf_counter()
        self.elapsed = self.stop - self.start
        return False

# 这里的timer是__enter__的返回值
with Timer() as timer:
    nums = []
    for n in range(10000):
        nums.append(n ** 2)

print(timer.elapsed)
```

# Mixin模式
Mixin模式是一种设计模式,将许多可以重用的功能写到类中当Mixin,凡是需要Mixin类功能的类都去通过多继承来获得Mixin类的功能.
```python
import json


class MapMixin:
    def __getitem__(self, key):
        return self.__dict__[key]

    def __setitem__(self, key, value):
        self.__dict__[key] = value


class DictMixin:
    def to_dict(self):
        return self.__convert_dict(self.__dict__)

    def __convert_dict(self, attrs: dict):
        result = {}
        for key, value in attrs.items():
            result[key] = self.__convert_value(value)

        return result

    def __convert_value(self, value):
        if isinstance(value, DictMixin):
            return value.to_dict()
        elif isinstance(value, dict):
            return self.__convert_dict(value)
        elif isinstance(value, list):
            return [self.__convert_value(v) for v in value]
        elif hasattr(value, '__dict__'):
            return self.__convert_dict(value.__dict__)
        else:
            return value


class JSONMixin:
    def to_json(self):
        return json.dumps(self.to_dict())


class Student(MapMixin, DictMixin, JSONMixin):
    def __init__(self, name, age):
        self.name = name
        self.age = age

# {"name": "Jack", "age": 20, "clasx": {"name": "class 9-1", "building": "A"}}

s = Student("Jack", 20)

print(s["name"])
print(s.to_dict())
print(s.to_json())

```

# 单例模式
单例模式的根本目的就是让一个类只能制造出一个对象
单例的需求一般是针对需要共享数据的对象,例如:工厂对象,数据库连接池对象,任何其他想要所有人共享的对象
```python
def singleton(cls):
    _instance = {}

    def inner(*args, **kwargs):
        if cls in _instance:
            return _instance[cls]

        obj = cls(*args, **kwargs)
        _instance[cls] = obj

        return obj

    return inner


class SingletonMeta(type):
    def __call__(cls, *args, **kwargs):
        if hasattr(cls, '_instance'):
            return getattr(cls, '_instance')

        obj = super().__call__(*args, **kwargs)
        setattr(cls, '_instance', obj)

        return obj


# @singleton
class Person(metaclass=SingletonMeta):
    pass


p_1 = Person()
p_2 = Person()

print(p_1 is p_2)
```