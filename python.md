- [python](#python)
  * [1、标准数据类型有哪些？](#1-----------)
  * [2、如何创建一个字典？](#2----------)
  * [3、shuashua那个下划线和单下划线的区别](#3-shuashua-------------)
  * [4、Python的自省机制](#4-python-----)
  * [5、文件可以使用for循环进行遍历？](#5-------for-------)
  * [6、迭代器和生成器的区别](#6-----------)
  * [7、`*args` 和 `**kwargs`](#7---args-------kwargs-)
  * [8、装饰器怎么用？装饰器解释下，基本要求是什么?](#8-----------------------)
  * [9、新式类和旧式类区别？](#9-----------)
  * [10、`__new__`和`__init__`的区别？](#10----new-------init-------)
  * [11、单例模式的几种实现方法？](#11-------------)
  * [12、作用域的类型有哪些？](#12-----------)
  * [13、深拷贝和浅拷贝的区别？](#13------------)
  * [14、多线程和多进程的区别？](#14------------)
  * [16、read,readline和readlines](#16-read-readline-readlines)
  * [17、闭包](#17---)
  * [18、垃圾回收机制](#18-------)
  * [19、+和join的区别？](#19---join----)
  * [20、为什么要使用Lambda函数？怎么使用？](#20-------lambda--------)
  * [21、协程的理解?怎么使用?](#21------------)
  * [22、谈下python的GIL?](#22---python-gil-)
  * [23、字典如何删除键和合并两个字典?](#23----------------)
  * [24、列出5个python标准库?](#24---5-python----)
  * [25、字典和json字符串相互转化方法？](#25----json----------)
  * [26、列表去重的方法?](#26---------)
  * [27、python2和python3的range（100）的区别？](#27-python2-python3-range-100-----)
  * [28、python2和python3区别？](#28-python2-python3---)
  * [29、列出几种魔术方法并简要介绍用途？](#29-----------------)
  * [30、异常的解释？](#30-------)
  * [31、sort函数内部实现原理？](#31-sort---------)
  * [32、如何提高python的运行效率?](#32-----python------)

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

## 12、作用域的类型有哪些？
- 局部作用域： 在函数中定义的变量
- 嵌套作用域： 为了实现Python的闭包
- 全局作用域： 作用范围仅限于单个模块文件内
- 内置作用域： 系统内固定模块里定义的变量
- 搜索变量名的优先级：局部作用域 > 嵌套作用域 > 全局作用域 > 内置作用域

## 13、深拷贝和浅拷贝的区别？

|代码|区别|
|:-:|:-:|
|`deepcopy`|深拷贝：对一个对象的拷贝做出改变时，不会影响原对象|
|`copy`|浅拷贝：在拷贝中改动，也会影响到原对象|

## 14、多线程和多进程的区别？
|多线程|多进程|
|:-:|:-:|
|`threading`|`multiprocessing`|
|共享全局变量|不共享全局变量|
|所有子线程的进程号相同|不同的子进程进程号不同|
|共享内存空间|内存是独立的|
|同一个进程的线程之间可以直接交流|两个进程想通信，必须通过一个中间代理来实现|
|创建新线程很简单|创建新进程需要对其父进程进行一次克隆|
|一个线程可以控制和操作同一进程里的其他线程|进程只能操作子进程|
|多线程中，所有变量都由所有线程共享|多进程中，同一个变量，各自有一份拷贝存在于每个进程中，互不影响|

##　15、is是对比地址,==是对比值!!

## 16、read,readline和readlines

|代码|意义|
|:-:|:-:|
|`read`|读取整个文件|
|`readline`|读取下一行,使用生成器方法|
|`readlines`|读取整个文件到一个迭代器以供我们遍历|

## 17、闭包
- 闭包形成的条件:
	1. 外部函数中定义了内部函数
	2. 外部函数有返回值
	3. 返回的值是：内部函数名
	4. 内部函数引用了外部函数的变量

```
def outer_func(a,b):
  c=10
  def inner_func():
    sum = a+b+c
    print('sum')
  return inner_func
# 使用
inner_func = outer_func(2,3)
inner_func()
```

## 18、垃圾回收机制
- GC主要使用引用计数来跟踪和回收垃圾。
- 在引用计数的基础上，通过"标记-清除”解决容器对象可能产生的循环引用问题，
- 通过"分代回收”以空间换时间的方法提高垃圾回收效率。

## 19、+和join的区别？

|代码|意义|
|:-:|:-:|
|`+`|可以连接多个字符串产生一个字符串对象,合并str1和str2，用str1+str2|
|`join`|将多个字符串采用固定的分隔符连接在一起,只会进行一次内存申请，因此运行效率相对于+会快很多。|

## 20、为什么要使用Lambda函数？怎么使用？
- 也称为丢弃函数，可以与其他预定义函数（filter(),map()等）一起使用。相对于定义的可重复使用的函数来说，这个函数更加简单便捷。

```
from functools import reduce
mylist = [2,3,4,5,6,7,8]
newlist_filter = list(filter(lambda a:(a/3==2),mylist))
newlist_map = list(map(lambda a:(a/3!=2),mylist))
newlist_reduce = reduce(lambda a,b: a+b,mylist)
print(newlist_filter) #[6]
print(newlist_map)  #[True,True,True,True,False,True,True]
print(newlist_reduce) # 35
```
## 21、协程的理解?怎么使用?
- 协程的作用：是在执行函数A时可以随时中断去执行函数B，然后中断函数B继续执行函数A（可以自由切换）。
- 但这一过程并不是函数调用，这一整个过程看似像多线程，然而协程只有一个线程执行。
- python2.x实现协程的方式有： yield + send gevent
- python3.x协程：asyncio + yield from (python3.4+)  asyncio + async/await (python3.5+)

## 22、谈下python的GIL?
- GIL 是python的全局解释器锁，同一进程中假如有多个线程运行，一个线程在运行python程序的时候会霸占python解释器（加了一把锁即GIL），使该进程内的其他线程无法运行，等该线程运行完后其他线程才能运行。如果线程运行过程中遇到耗时操作，则解释器锁解开，使其他线程运行。所以在多线程中，线程的运行仍是有先后顺序的，并不是同时进行。
多进程中因为每个进程都能被系统分配资源，相当于每个进程有了一个python解释器，所以多进程可以实现多个进程的同时运行，缺点是进程系统资源开销大

## 23、字典如何删除键和合并两个字典?
- del和update方法

## 24、列出5个python标准库?
- os sys re math datetime
去首尾空格： a.strip()
去空格：replace 或 split

## 25、字典和json字符串相互转化方法？
- json.dumps()：字典 转 json字符串；
- json.loads()：json 转 字典

## 26、列表去重的方法?
1. set集合去重
2. fromkeys:用列表中的元素作为字典中的key生成一个新字典，然后获取字典的key
3. 引入defaultdict
4. 最简单的循环，添加入新的列表，如果新列表中没有相同元素，则加入
5. 引入itertools的groupby方法
6. reduce方法

## 27、python2和python3的range（100）的区别？
- python2返回列表，python3返回迭代器，节约内存

## 28、python2和python3区别？
1. Python3 使用 print 必须要以小括号包裹打印内容，比如 print('hi')
Python2 既可以使用带小括号的方式，也可以使用一个空格来分隔打印内容，比如 print 'hi'
2. python2 range(1,10)返回列表，python3中返回迭代器，节约内存
3. python2中使用ascii编码，python中使用utf-8编码
4. python2中unicode表示字符串序列，str表示字节序列
 python3中str表示字符串序列，byte表示字节序列
5. python2中为正常显示中文，引入coding声明，python3中不需要
6. python2中是raw_input()函数，python3中是input()函数
## 29、列出几种魔术方法并简要介绍用途？
- `__init__`:对象初始化方法
- `__new__`:创建对象时候执行的方法，单列模式会用到
- `__str__`:当使用print输出对象的时候，只要自己定义了`__str__(self)`方法，那么就会打印从在这个方法中return的数据
- `__del__`:删除对象执行的方法

## 30、异常的解释？
- `IOError`：输入输出异常
- `AttributeError`：试图访问一个对象没有的属性
- `ImportError`：无法引入模块或包，基本是路径问题
- `IndentationError`：语法错误，代码没有正确的对齐
- `IndexError`：下标索引超出序列边界
- `KeyError`:试图访问你字典里不存在的键
- `SyntaxError`:Python代码逻辑语法出错，不能执行
- `NameError`:使用一个还未赋予对象的变量

## 31、sort函数内部实现原理？
- 内部实现是 timsort,Timsort是结合了合并排序和插入排序而得出的排序算法，它在现实中有很好的效率。
该算法找到数据中已经排好序的块-分区，每一个分区叫一个run，然后按规则合并这些run。
- 算法的过程包括：
	1. 如果数组长度小于某个值，直接用二分插入排序算法
	2. 找到各个run，并入栈
	3. 按规则合并run

## 32、如何提高python的运行效率?
1. 使用生成器，因为可以节约大量内存
2. 循环代码优化，避免过多重复代码的执行
3. 核心模块用Cython  PyPy等，提高效率
4. 多进程,多线程,协程
5. 多个if elif条件判断，可以把最有可能先发生的条件放到前面写，这样可以减少程序判断的次数，提高效率
