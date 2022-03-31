- [python](#python)
  * [1、标准数据类型有哪些？](#1-----------)
  * [2、如何创建一个字典？](#2----------)

# python

## 1、标准数据类型有哪些？
- 【不可变对象】：不允许变量的值发生变化，如果改变了变量的值，相当于是新建了一个对象，而对于相同的值的对象，在内存中则只有一个对象（一个地址）
- 【可变对象】：允许变量的值发生变化，即如果对变量进行append.+=等这种操作后，只是改变了变量的值，而不会新建一个对象，变量引用的对象的地址也不会变化;
每个对象都有自己的地址

|数据类型|变化|
|:-:|:-:|
|Number（数字）|不可变|
|String（字符串）|不可变|
|Tuple（元组）|不可变|
|List（列表）|可变|
|Set（集合）|可变|
|Dictionary（字典）|可变|


## 2、如何创建一个字典？

|方式|代码|
|:-:|:-:|
|传入关键字|`dict(a='1', b='2', c='3')`|
|映射函数|`dict(zip(['one', 'two', 'three'], [1, 2, 3]))`|
|可迭代对象|`dict([('one', 1), ('two', 2), ('three', 3)])`|

## 3、shuashua那个下划线和单下划线的区别

|变量|区别|
|:-:|:-:|
|`__xxx__`|特殊变量，可以直接访问|
|`__xxx`|私有变量，内部可以访问，外部可以通过`_${classname}__name`来访问|
|`_xxx`|口头私有变量,外部是可以访问的;但是请把我视为私有变量，不要随意访问|

## 4、Python的自省机制
自省机制：运行时能够获知对象的类型。

|函数|意义|
|:-:|:-:|
|`dir(object)`|返回对象的属性名称|
|`type(object)`|返回对象的类型|
|`hasattr(object,'attr')`|判断一个对象的属性值是否存在|
|`getattr(object,'attr')`|获得一个对象的属性值|
|`isinstance("string",str)`|确定是否是特定类型的实例|

## 5、文件可以使用for循环进行遍历？
文件对象实现了迭代器协议

## 6、迭代器和生成器的区别
生成器是一种特殊的迭代器。

|类型|创建|区别|
|:-:|:-:|:-:|
|生成器|通过函数调用`vield`或`()`的形式创建|调用`next()`函数或`for`循环中，所有过程被执行，且返回值；只能遍历一次，好处是延迟计算，一次返回一个结果，不会一次生成所有结果，对大数据处理有利。|
|迭代器|通过`iter()`内置函数创建|调用`next()`函数或`for`循环中，所有值被返回，没有其他过程或动作。|

## 7、`*args` 和 `**kwargs`

|参数|意义|
|:-:|:-:|
|`*args`|不确定函数里要传递多少参数|
|`**kwargs`|允许使用没有事先定义的参数名|

## 8、装饰器怎么用？装饰器解释下，基本要求是什么?
- ➤装饰器的作用就是为已经存在的对象添加额外的功能。参数为函数，返回为函数，本质是嵌套函数，可以传参，也可以不用传参
- ➤`@property`: 把类内方法当成属性来使用，必须要有返回值，相当于getter.简而言之就是可以在调用的时候不用加()
- ➤`@staticmethod`  不需要表示自身对象的self和自身类的cls参数，就和使用普通的函数一样。简而言之，在类里有@staticmethod的，可以直接调用，没有加上改装饰器的方法就不能去调用。
- ➤`@classmethod`  不需要self参数，但是第一个参数需要表示自身类的cls参数。在类里的所有方法都可以调用的。

## 9、新式类和旧式类区别？

- 新式类都从object继承，经典类不需要。
- 新式类的MRO(method resolution order 基类搜索顺序)算法采用C3算法广度优先搜索，而旧式类的MRO算法是采用深度优先搜索。
- 新式类相同父类只执行一次构造函数，经典类重复执行多次。

## 10、`__new__`和`__init__`的区别？

|方法|区别|
|:-:|:-:|
|`__new__`|静态方法,返回一个创建的实例|
|`__init__`|实例方法,不返回,|

- 只有在__new__返回一个cls的实例时后面的__init__才能被调用.
- 当创建一个新实例时调用__new__,初始化一个实例时用__init__.

## 11、单例模式的几种实现方法？
单例模式：简单地说就是全局只有一个的类对象。

1. 使用模块
```
# a.py
class Singleton(object):
    def foo(self):
        pass
singleton = Singleton()
```
```
from a import singleton
```
2. 使用装饰器
```
def Singleton(cls):
    _instance = {}
    def _singleton(*args, **kargs):
        if cls not in _instance:
            _instance[cls] = cls(*args, **kargs)
        return _instance[cls]
    return _singleton
@Singleton
class A(object):
    a = 1
    def __init__(self, x=0):
        self.x = x
a1 = A(2)
a2 = A(3)
```
3. 使用类
```
# 按照以此方式创建的单例，无法支持多线程
class Singleton(object):
    def __init__(self):
        pass
    @classmethod
    def instance(cls, *args, **kwargs):
        if not hasattr(Singleton, "_instance"):
            Singleton._instance = Singleton(*args, **kwargs)
        return Singleton._instance
```
```
# 解决办法：加锁！未加锁部分并发执行,加锁部分串行执行,速度降低,但是保证了数据安全，可以支持多线程的单例模式，这种方式实现的单例模式，使用时会有限制，以后实例化必须通过 obj = Singleton.instance()
如果用 obj=Singleton() ,这种方式得到的不是单例。
import time
import threading
class Singleton(object):
    _instance_lock = threading.Lock()
    def __init__(self):
        time.sleep(1)
    @classmethod
    def instance(cls, *args, **kwargs):
        if not hasattr(Singleton, "_instance"):
            with Singleton._instance_lock:
                if not hasattr(Singleton, "_instance"):
                    Singleton._instance = Singleton(*args, **kwargs)
        return Singleton._instance
def task(arg):
    obj = Singleton.instance()
    print(obj)
for i in range(10):
    t = threading.Thread(target=task,args=[i,])
    t.start()
time.sleep(20)
obj = Singleton.instance()
print(obj)
```
4. 基于__new__方法实现（推荐使用，方便）
```
# 采用这种方式的单例模式，以后实例化对象时，和平时实例化对象的方法一样 obj = Singleton()
import threading
class Singleton(object):
    _instance_lock = threading.Lock()
    def __init__(self):
        pass
    def __new__(cls, *args, **kwargs):
        if not hasattr(Singleton, "_instance"):
            with Singleton._instance_lock:
                if not hasattr(Singleton, "_instance"):
                    Singleton._instance = object.__new__(cls)  
        return Singleton._instance
obj1 = Singleton()
obj2 = Singleton()
print(obj1,obj2)
def task(arg):
    obj = Singleton()
    print(obj)
for i in range(10):
    t = threading.Thread(target=task,args=[i,])
    t.start()
```
5. 基于metaclass方式实现
- 类由`type`创建，创建类时，`type`的`__init__`方法自动执行，类`()` 执行`type`的 `__call__`方法(类的`__new__`方法,类的`__init__`方法)
- 对象由类创建，创建对象时，类的`__init__`方法自动执行，对象`()`执行类的`__call__`方法

```
# 例子
class Foo:
    def __init__(self):
        pass

    def __call__(self, *args, **kwargs):
        pass

obj = Foo()
# 执行type的 __call__ 方法，调用 Foo类（是type的对象）的 __new__方法，用于创建对象，然后调用 Foo类（是type的对象）的 __init__方法，用于对对象初始化。

obj()    # 执行Foo的 __call__ 方法    

```

```
# 元类的使用
class SingletonType(type):
    def __init__(self,*args,**kwargs):
        super(SingletonType,self).__init__(*args,**kwargs)

    def __call__(cls, *args, **kwargs): # 这里的cls，即Foo类
        print('cls',cls)
        obj = cls.__new__(cls,*args, **kwargs)
        cls.__init__(obj,*args, **kwargs) # Foo.__init__(obj)
        return obj

class Foo(metaclass=SingletonType): # 指定创建Foo的type为SingletonType
    def __init__(self，name):
        self.name = name
    def __new__(cls, *args, **kwargs):
        return object.__new__(cls)

obj = Foo('xx')
```
```
# 单例模式
import threading

class SingletonType(type):
    _instance_lock = threading.Lock()
    def __call__(cls, *args, **kwargs):
        if not hasattr(cls, "_instance"):
            with SingletonType._instance_lock:
                if not hasattr(cls, "_instance"):
                    cls._instance = super(SingletonType,cls).__call__(*args, **kwargs)
        return cls._instance

class Foo(metaclass=SingletonType):
    def __init__(self,name):
        self.name = name


obj1 = Foo('name')
obj2 = Foo('name')
print(obj1,obj2)
```
