



## 字符串和变量

### 数据类型

#### 整数

Python可以处理任意大小的整数，当然包括负整数，在程序中的表示方法和数学上的写法一模一样；十六进制用```0x```前缀和0-9，a-f表示

#### 浮点数【小数】

#### 字符串

#### 布尔值

#### 空值【None】

空值是Python里一个特殊的值，用`none`表述

#### 列表【list】**

> 有序集合

```python
classmates = ['Michael', 'Bob', 'Tracy']
classmates[0] #'Michael'
classmates[-1] # 'Tracy'
```

- **往list中追加元素到末尾**

`classmates.append('Adam')`

- **也可以把元素插入到指定的位置**

`classmates.insert(1, 'Jack')`

- **删除list末尾的元素**

`classmates.pop()`

- **删除指定位置的元素**

`classmates.pop(1)`

- **把某个元素替换成别的元素**

`classmates[1] = 'Sarah'`

#### tuple元组 **

> ***tuple一旦初始化就不能修改，即tuple的每个元素，指向永远不变***

```python
classmates = ('Michael', 'Bob', 'Tracy')
classmates[0]
classmates[-1]
```

- **定义只有一个元素的元组：**

`t=(1,)`

#### 字典【dict】  **

> **键值对存储，具备极快的查找速度**
>
> **key必须是不可变对象，key唯一**

`d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}`

取值：1、`d['Bob']`

​				2、`d.get('Bob')`

- **删除key**

`d.pop('Bob')`

> **set**
>
> > **set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key。**
> >
> > 要创建一个set，需要提供一个list作为输入集合：
> >
> > `s = set([1, 2, 3])`
> >
> > - 添加元素
> >
> > `s.add(4)`
> >
> > - 删除元素
> >
> > `s.remove(1)`

### 变量

> **变量名必须是大小写英文、数字和`_`的组合，且不能用数字开头**

### 常量

在Python中，通常用全部大写的变量名表示常量

## 字符串编码

`str`和`byte`相互转换时，需指定编码格式

`byte`转换`str`：`b'ABC'.decode('utf-8')`

`str`转换`byte`：`'中文'.encode('utf-8')`

字符长度函数：`len('ABC')`

### 占位符

```python
'Hi, %s, you have %d dollars.' % ('Michael', 1000000)
```

| 占位符 |  替换内容  |
| :----: | :--------: |
|   %d   |    整数    |
|   %f   |   浮点数   |
|   %s   |   字符串   |
|   %x   | 十六进制数 |

```python
'Hello, {0}, 成绩提升了 {1:.1f}%'.format('小明', 17.125)
```



## 条件判断

```python
age = 3
if age >= 18:
    print('adult')
elif age >= 6:
    print('teenager')
else:
    print('kid')
```

## 循环

```python
# for...in... 循环
sum = 0
for x in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]:
    sum = sum + x
print(sum)
```

```python
# while 循环
sum = 0
n = 99
while n > 0:
    sum = sum + n
    n = n - 2
print(sum)
```



### break和continue

- **break退出当前循环**

```python
n = 1
while n <= 100:
    if n > 10: # 当n = 11时，条件满足，执行break语句
        break # break语句会结束当前循环
    print(n)
    n = n + 1
print('END')
```

- **continue跳过当前循环，开始下一轮循环**

```python
n = 0
while n < 10:
    n = n + 1
    if n % 2 == 0: # 如果n是偶数，执行continue语句
        continue # continue语句会直接继续下一轮循环，后续的print()语句不会执行
    print(n)
```

***

## 数据类型转换

```python
>>> int('123')
123
>>> int(12.34)
12
>>> float('12.34')
12.34
>>> str(1.23)
'1.23'
>>> str(100)
'100'
>>> bool(1)
True
>>> bool('')
False
```

## 函数参数  **

> **参数定义的顺序必须是：必选参数、默认参数、可变参数、命名关键字参数和关键字参数**

1. 必选参数

```python
def power(x, n):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s
```

2. 默认参数

```python
def power(x, n=2):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s
```

> **默认参数必须指向不变对象！**

```python
def add_end(L=[]): # L是list，可变
    L.append('END')
    return L

>>> add_end()
['END']
>>> add_end()
['END', 'END']
>>> add_end()
['END', 'END', 'END']
# 正确写法
def add_end(L=None):
    if L is None:
        L = []
    L.append('END')
    return L
```

3. 可变参数

```python
def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum
```

> **Python允许你在list或tuple前面加一个`*`号，把list或tuple的元素变成可变参数传进去**

4. 关键字参数

>  ***可变参数允许你传入0个或任意个参数，这些可变参数在函数调用时自动组装为一个tuple。而关键字参数允许你传入0个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个dict***

```python
def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)
    
>>> person('Adam', 45, gender='M', job='Engineer')
name: Adam age: 45 other: {'gender': 'M', 'job': 'Engineer'}
            
>>> extra = {'city': 'Beijing', 'job': 'Engineer'}
>>> person('Jack', 24, **extra)
name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}
# **extra表示把extra这个dict的所有key-value用关键字参数传入到函数的**kw参数，kw将获得一个dict，注意kw获得的dict是extra的一份拷贝，对kw的改动不会影响到函数外的extra
```



5. 命名关键字参数

```python
def person(name, age, *, city, job):
    print(name, age, city, job)
```

> **如果函数定义中已经有了一个可变参数，后面跟着的命名关键字参数就不再需要一个特殊分隔符`*`了**
>
> <u>***命名关键字参数必须传入参数名***</u>
>
> ```python
> def person(name, age, *args, city, job):
>    	print(name, age, args, city, job)
> ```

- 命名关键字参数可以有缺省值

```python
def person(name, age, *, city='Beijing', job):
    print(name, age, city, job)
    
>>> person('Jack', 24, job='Engineer')
Jack 24 Beijing Engineer
```

***

> **小结：**
>
> Python的函数具有非常灵活的参数形态，既可以实现简单的调用，又可以传入非常复杂的参数。
>
> 默认参数一定要用不可变对象，如果是可变对象，程序运行时会有逻辑错误！
>
> 要注意定义可变参数和关键字参数的语法：
>
> `*args`是可变参数，args接收的是一个tuple；
>
> `**kw`是关键字参数，kw接收的是一个dict。
>
> 以及调用函数时如何传入可变参数和关键字参数的语法：
>
> 可变参数既可以直接传入：`func(1, 2, 3)`，又可以先组装list或tuple，再通过`*args`传入：`func(*(1, 2, 3))`；
>
> 关键字参数既可以直接传入：`func(a=1, b=2)`，又可以先组装dict，再通过`**kw`传入：`func(**{'a': 1, 'b': 2})`。
>
> 使用`*args`和`**kw`是Python的习惯写法，当然也可以用其他参数名，但最好使用习惯用法。
>
> 命名的关键字参数是为了限制调用者可以传入的参数名，同时可以提供默认值。
>
> 定义命名的关键字参数在没有可变参数的情况下不要忘了写分隔符`*`，否则定义的将是位置参数。

## 递归函数

> ***如果一个函数在内部调用自身本身，这个函数就是递归函数***

```python
def fact(n):
    if n==1:
        return 1
    return n * fact(n - 1)

>>> fact(1)
1
>>> fact(5)
120
```

> 解决递归调用栈溢出，使用尾递归
>
> - 尾递归指定是，在函数返回的时候，调用自身本身，并且，return语句不能包含表达式
>
> ```python
> def fact(n):
>     return fact_iter(n, 1)
> 
> def fact_iter(num, product):
>     if num == 1:
>         return product
>     return fact_iter(num - 1, num * product)
> ```
>
> >  遗憾的是，大多数编程语言没有针对尾递归做优化，Python解释器也没有做优化，所以，即使把上面的`fact(n)`函数改成尾递归方式，也会导致栈溢出。

## 切片

1. 取一个list或tuple的部分元素是非常常见的操作

```python
>>> L = ['Michael', 'Sarah', 'Tracy', 'Bob', 'Jack']
>>> L[0:3] # L[0:3]表示，从索引0开始取，直到索引3为止，但不包括索引3
['Michael', 'Sarah', 'Tracy']

>>> L[:3] # 如果第一个索引是0，还可以省略
['Michael', 'Sarah', 'Tracy']

>>> L[-2:] # 取倒数前两个元素
['Bob', 'Jack']
>>> L[-2:-1] # 取倒数第二个元素，不包括倒数第一个元素
['Bob']
>>> L[::2] # 每隔两个取一个
```

> - **tuple也是一种list，唯一区别是tuple不可变。因此，tuple也可以用切片操作，只是操作的结果仍是tuple**
>
> ```python
> >>> (0, 1, 2, 3, 4, 5)[:3]
> (0, 1, 2)
> ```
>
> - **字符串`'xxx'`也可以看成是一种list，每个元素就是一个字符。因此，字符串也可以用切片操作，只是操作结果仍是字符串**
>
> ```python
> >>> 'ABCDEFG'[:3]
> 'ABC'
> >>> 'ABCDEFG'[::2]
> 'ACEG'
> ```
>
> 

## 迭代

> 默认情况下，dict迭代的是key。如果要迭代value，可以用`for value in d.values()`，如果要同时迭代key和value，可以用`for k, v in d.items()`

- 如何判断一个对象是否可迭代？

```python
# 通过collections模块的Iterable类型判断：
>>> from collections import Iterable
>>> isinstance('abc', Iterable) # str是否可迭代
True
>>> isinstance([1,2,3], Iterable) # list是否可迭代
True
>>> isinstance(123, Iterable) # 整数是否可迭代
Fals
```

## 列表生成式

- 写列表生成式时，把要生成的元素`x * x`放到前面，后面跟`for`循环，就可以把list创建出来

```python
>>> [x * x for x in range(1, 11)]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

>>> [m + n for m in 'ABC' for n in 'XYZ'] # for循环嵌套
['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']

>>> [x * x for x in range(1, 11) if x % 2 == 0] # for循环加if条件
[4, 16, 36, 64, 100]

>>> d = {'x': 'A', 'y': 'B', 'z': 'C' }
>>> [k + '=' + v for k, v in d.items()]
['y=B', 'x=A', 'z=C']
```

## 生成器

- 第一种简单方法，将列表生成式的`[]`换成`()`即可

`g = (x * x for x in range(10))`

> ***知识点***
>
> ```python
> a, b = b, a + b
> #  相当于
> t = (b, a + b) # t是一个tuple
> a = t[0]
> b = t[1]
> ```

- **如果一个函数定义中包含`yield`关键字，那么这个函数就不再是一个普通函数，而是一个generator**

```python
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a + b
        n = n + 1
    return 'done'
```

> **generator的函数，在每次调用`next()`的时候执行，遇到`yield`语句返回，再次执行时从上次返回的`yield`语句处继续执行**
>
> ```python
> def odd():
>    	print('step 1')
>    	yield 1
>    	print('step 2')
>    	yield(3)
>    	print('step 3')
>    	yield(5)
>    
> >>> o = odd()
> >>> next(o)
> step 1
> 1
> >>> next(o)
> step 2
> 3
> >>> next(o)
> step 3
> 5
> >>> next(o)
> Traceback (most recent call last):
>   File "<stdin>", line 1, in <module>
> StopIteration
> ```

## 迭代器 **

> - 凡是可作用于`for`循环的对象都是`Iterable`类型；
>
> + 凡是可作用于`next()`函数的对象都是`Iterator`类型，它们表示一个惰性计算的序列；
>
> - 集合数据类型如`list`、`dict`、`str`等是`Iterable`但不是`Iterator`，不过可以通过`iter()`函数获得一个`Iterator`对象。

## Python内置函数map()、reduce()、filter()、sorted()

- **map函数**

> **`map()`函数接收两个参数，一个是函数，一个是`Iterable`，`map`将传入的函数依次作用到序列的每个元素，并把结果作为新的`Iterator`返回**

```python
>>> def f(x):
...     return x * x
...
>>> r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> list(r)
[1, 4, 9, 16, 25, 36, 49, 64, 81]
```

**`map()`传入的第一个参数是`f`，即函数对象本身。由于结果`r`是一个`Iterator`，`Iterator`是惰性序列，因此通过`list()`函数让它把整个序列都计算出来并返回一个list**

- **reduce函数**

> **`reduce`把一个函数作用在一个序列`[x1, x2, x3, ...]`上，这个函数必须接收两个参数，`reduce`把结果继续和序列的下一个元素做累积计算，其效果就是：**
>
> `reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)`

```python
# 比方说对一个序列求和，就可以用reduce实现：
>>> from functools import reduce
>>> def add(x, y):
...     return x + y
...
>>> reduce(add, [1, 3, 5, 7, 9])
25
```

- **filter函数**

> **和`map()`类似，`filter()`也接收一个函数和一个序列。和`map()`不同的是，`filter()`把传入的函数依次作用于每个元素，然后根据返回值是`True`还是`False`决定保留还是丢弃该元素**

```python
# 过滤序列中的偶数
def is_odd(n):
    return n % 2 == 1

list(filter(is_odd, [1, 2, 4, 5, 6, 9, 10, 15]))
# 结果: [1, 5, 9, 15]
```

- **sorted排序函数**

```python
>>> sorted([36, 5, -12, 9, -21])
[-21, -12, 5, 9, 36]

# 还可以接收一个key函数来实现自定义的排序，例如按绝对值大小排序
>>> sorted([36, 5, -12, 9, -21], key=abs)
[5, 9, -12, -21, 36]

# 反向排序，可以传入第三个参数reverse=True
>>> sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower, reverse=True)
['Zoo', 'Credit', 'bob', 'about']
```

## 闭包 **

> ```python
> def lazy_sum(*args):
>    	def sum():
>    		ax = 0
>    		for n in args:
>    			ax = ax + n
>    		return ax
>    	return sum
> ```
>
> **我们在函数`lazy_sum`中又定义了函数`sum`，并且，内部函数`sum`可以引用外部函数`lazy_sum`的参数和局部变量，当`lazy_sum`返回函数`sum`时，相关参数和变量都保存在返回的函数中，这种称为“闭包（Closure）”**

```python
def count():
    fs = []
    for i in range(1, 4):
        def f():
             return i*i
        fs.append(f)
    return fs

if __name__ == '__main__':
    for f in count():
        print(f()) # 结果：9 9 9 而非1 4 9
```

> **返回函数不要引用任何循环变量，或者后续会发生变化的变量**

```python
def count():
    def f(j):
        def g():
            return j*j
        return g
    fs = []
    for i in range(1, 4):
        fs.append(f(i)) # f(i)立刻被执行，因此i的当前值被传入f()
    return fs

if __name__ == '__main__':
    for f in count():
        print(f()) # 1 4 9
```

## 匿名函数 lambda

- **定义：`lambda x:x*x`【冒号前的x表示参数，后面是返回表达式的结果，且只能返回表达式只有一个，不能写return】**

## 装饰器 **

> **代码运行期间动态增加功能的方式，称之为“装饰器”（Decorator）**

```python
def log1(func):
    def wrapper(*args,**kwargs):
        print('call %s()' %func.__name__)
        return func(*args,**kwargs)
    return wrappe
r
# 装饰器可传入参数
def log2(text):
    def decorator(func):
        def wrapper(*args,**kwargs):
            print(text,func.__name__)
            return func(*args,**kwargs)
        return wrapper
    return decorator

@log2('excute')
@log1
def now():
    print('2020年7月20日16:32:31')
    
if __name__ == '__main__':
    now()
```

## 类-Class

```python
class Student(object):

    def __init__(self, name, score):
        self.name = name
        self.score = score
```

> 判断对象类型：`type()`
>
> ```python
> >>> import types
> >>> def fn():
> ...     pass
> ...
> >>> type(fn)==types.FunctionType
> True
> >>> type(abs)==types.BuiltinFunctionType
> True
> >>> type(lambda x: x)==types.LambdaType
> True
> >>> type((x for x in range(10)))==types.GeneratorType
> True
> ```

> `isinstance()`
>
> ```python
> >>> isinstance('a', str)
> True
> >>> isinstance(123, int)
> True
> >>> isinstance(b'a', bytes)
> True
> 
> object -> Animal -> Dog -> Husky
> >>> a = Animal()
> >>> d = Dog()
> >>> h = Husky()
> >>> isinstance(h, Husky)
> True
> >>> isinstance(h, Dog)
> True
> 
> >>> isinstance([1, 2, 3], (list, tuple))
> True
> >>> isinstance((1, 2, 3), (list, tuple))
> True
> ```

> 获取对象的属性和方法：`dir()`
>
> ```python
> >>> dir('ABC')
> ['__add__', '__class__',..., '__subclasshook__', 'capitalize', 'casefold',..., 'zfill']
> ```

> 使用`getattr(),setattr(),hasattr()`
>
> ```python
> >>> class MyObject(object):
> ...     def __init__(self):
> ...         self.x = 9
> ...     def power(self):
> ...         return self.x * self.x
> ...
> >>> obj = MyObject()
> 
> >>> hasattr(obj, 'x') # 有属性'x'吗？
> True
> >>> obj.x
> 9
> >>> hasattr(obj, 'y') # 有属性'y'吗？
> False
> >>> setattr(obj, 'y', 19) # 设置一个属性'y'
> >>> hasattr(obj, 'y') # 有属性'y'吗？
> True
> >>> getattr(obj, 'y') # 获取属性'y'
> 19
> >>> obj.y # 获取属性'y'
> 19
> >>> hasattr(obj, 'power') # 有属性'power'吗？
> True
> >>> getattr(obj, 'power') # 获取属性'power'
> <bound method MyObject.power of <__main__.MyObject object at 0x10077a6a0>>
> >>> fn = getattr(obj, 'power') # 获取属性'power'并赋值到变量fn
> >>> fn # fn指向obj.power
> <bound method MyObject.power of <__main__.MyObject object at 0x10077a6a0>>
> >>> fn() # 调用fn()与调用obj.power()是一样的
> 81
> ```

> `__slots__`限制绑定实例的属性
>
> ```python
> class Student(object):
> 	__slots__ = ('name', 'age') # 用tuple定义允许绑定的属性名称
>     
> >>> s = Student() # 创建新的实例
> >>> s.name = 'Michael' # 绑定属性'name'
> >>> s.age = 25 # 绑定属性'age'
> >>> s.score = 99 # 绑定属性'score'
> Traceback (most recent call last):
> 	File "<stdin>", line 1, in <module>
> AttributeError: 'Student' object has no attribute 'score'
> ```

> `@property`使用：
>
> ```python
> # 把一个getter方法变成属性，只需要加上@property就可以了，此时，@property本身又创建了另一个装饰器@score.setter，负责把一个setter方法变成属性赋值
> class Student(object):
> 
>     @property
>     def score(self):
>         return self._score
> 
>     @score.setter
>     def score(self, value):
>         if not isinstance(value, int):
>             raise ValueError('score must be an integer!')
>         if value < 0 or value > 100:
>             raise ValueError('score must between 0 ~ 100!')
>         self._score = value
>         
> class Student(object):
> 
>     @property
>     def birth(self):
>         return self._birth
> 
>     @birth.setter
>     def birth(self, value):
>         self._birth = value
> 
>     @property
>     def age(self):
>         return 2015 - self._birth
> # 上面的birth是可读写属性，而age就是一个只读属性
> ```

## 多继承

```python
class Animal(object):
    pass

# 大类:
class Mammal(Animal):
    pass

class Bird(Animal):
    pass

# 各种动物:
class Dog(Mammal):
    pass

class Bat(Mammal):
    pass

class Parrot(Bird):
    pass

class Ostrich(Bird):
    pass

class Runnable(object):
    def run(self):
        print('Running...')

class Flyable(object):
    def fly(self):
        print('Flying...')
        
# 多继承
class Dog(Mammal, Runnable):
    pass

class Bat(Mammal, Flyable):
    pass
```

## 类中的特殊函数

### `__str__`

```python
>>> class Student(object):
...     def __init__(self, name):
...         self.name = name
...     def __str__(self):
...         return 'Student object (name: %s)' % self.name
...
>>> print(Student('Michael'))
Student object (name: Michael)
```

> ```python
> >>> s = Student('Michael')
> >>> s
> <__main__.Student object at 0x109afb310>
> ```
>
> 直接显示变量调用的不是`__str__()`，而是`__repr__()`，两者的区别是`__str__()`返回用户看到的字符串，而`__repr__()`返回程序开发者看到的字符串，也就是说，`__repr__()`是为调试服务的
>
> 通常`__str__()`和`__repr__()`代码都是一样的，所以，类中加一行代码：`__repr__=__str__`即可

### `__iter__`

> 如果一个类想被用于`for ... in`循环，类似list或tuple那样，就必须实现一个`__iter__()`方法，该方法返回一个迭代对象，然后，Python的for循环就会不断调用该迭代对象的`__next__()`方法拿到循环的下一个值，直到遇到`StopIteration`错误时退出循环

```python
class Fib(object):
    def __init__(self):
        self.a, self.b = 0, 1 # 初始化两个计数器a，b

    def __iter__(self):
        return self # 实例本身就是迭代对象，故返回自己

    def __next__(self):
        self.a, self.b = self.b, self.a + self.b # 计算下一个值
        if self.a > 100000: # 退出循环的条件
            raise StopIteration()
        return self.a # 返回下一个值
```

### `__getitem__`

```python
class Fib(object):
    def __getitem__(self, n):
        a, b = 1, 1
        for x in range(n):
            a, b = b, a + b
        return a

>>> f = Fib()
>>> f[0]
1
>>> f[1]
1
>>> f[2]
2
>>> f[3]
3
>>> f[10]
89
>>> f[100]
573147844013817084101
```

### `__getattr__`

> 调用类中不存在的属性或函数，会抛异常；加上`__getattr__`函数，调用类中不存在的属性或函数，会返回函数值
>
> ```python
> class Student(object):
>    	def __init__(self):
>    		self.name = 'Michael'
> 
>    	def __getattr__(self, attr):
>    		if attr=='score':
>    			return 99
>    
> >>> s = Student()
> >>> s.name
> 'Michael'
> >>> s.score
> 99
> ```

### `__call__`

> **可直接调用函数一样，调用实例对象**
>
> ```python
> class Student(object):
>    	def __init__(self, name):
>    		self.name = name
> 
>    	def __call__(self):
>             print('My name is %s.' % self.name)
>    
> >>> s = Student('Michael')
> >>> s() # self参数不要传入
> My name is Michael.
> ```
>
> **通过`callable()`函数，我们就可以判断一个对象是否是“可调用”对象**

## 枚举类

```python
from enum import Enum, unique

@unique
class Weekday(Enum):
    Sun = 0 # Sun的value被设定为0
    Mon = 1
    Tue = 2
    Wed = 3
    Thu = 4
    Fri = 5
    Sat = 6
    
>>> day1 = Weekday.Mon
>>> print(day1)
Weekday.Mon
>>> print(Weekday.Tue)
Weekday.Tue
>>> print(Weekday['Tue'])
Weekday.Tue
>>> print(Weekday.Tue.value)
2
>>> print(day1 == Weekday.Mon)
True
>>> print(day1 == Weekday.Tue)
False
>>> print(Weekday(1))
Weekday.Mon
>>> print(day1 == Weekday(1))
True
>>> Weekday(7)
Traceback (most recent call last):
  ...
ValueError: 7 is not a valid Weekday
>>> for name, member in Weekday.__members__.items():
...     print(name, '=>', member)
...
Sun => Weekday.Sun
Mon => Weekday.Mon
Tue => Weekday.Tue
Wed => Weekday.Wed
Thu => Weekday.Thu
Fri => Weekday.Fri
Sat => Weekday.Sat
```

## type函数创建类

```python
>>> def fn(self, name='world'): # 先定义函数
...     print('Hello, %s.' % name)
...
>>> Hello = type('Hello', (object,), dict(hello=fn)) # 创建Hello class
```

> `type`函数的三个参数依次是：
>
> 1. class的名称
> 2. 继承的父类集合，注意Python支持多重继承，如果只有一个父类，别忘了tuple的单元素写法
> 3. class的方法名称与函数绑定，这里我们把函数`fn`绑定到方法名`hello`上

## 异常处理

```python
try:
    print('try...')
    r = 10 / int('a')
    print('result:', r)
except ValueError as e:
    print('ValueError:', e)
except ZeroDivisionError as e:
    print('ZeroDivisionError:', e)
finally:
    print('finally...')
print('END')
```

```python
def foo(s):
    n=int(s)
    if n == 0:
        raise ValueError('invalid value %s' % s)
    return 10/n

def bar():
    try:
        foo('0')
    except ValueError as e:
        print('ValueError!')
        raise # 继续往上抛异常

if __name__ == "__main__":
    bar()
    
# 输出
ValueError: invalid value 0
ValueError!
```

## 单元测试

**被测试类**

```python
class Dict(dict):

    def __init__(self, **kw):
        super().__init__(**kw)

    def __getattr__(self, key):
        try:
            return self[key]
        except KeyError:
            raise AttributeError(r"'Dict' object has no attribute '%s'" % key)

    def __setattr__(self, key, value):
        self[key] = value
```

**测试类**

```python
import unittest

from mydict import Dict

class TestDict(unittest.TestCase):

    def test_init(self):
        d = Dict(a=1, b='test')
        self.assertEqual(d.a, 1)
        self.assertEqual(d.b, 'test')
        self.assertTrue(isinstance(d, dict))

    def test_key(self):
        d = Dict()
        d['key'] = 'value'
        self.assertEqual(d.key, 'value')

    def test_attr(self):
        d = Dict()
        d.key = 'value'
        self.assertTrue('key' in d)
        self.assertEqual(d['key'], 'value')

    def test_keyerror(self):
        d = Dict()
        with self.assertRaises(KeyError):
            value = d['empty']

    def test_attrerror(self):
        d = Dict()
        with self.assertRaises(AttributeError):
            value = d.empty
```

## 文件读写

```python
# 写文件
with open('E:\git-clone\zhaoya-git\dev1.txt','w',encoding='utf-8') as f: # w 覆盖更新；a 追加内容 
	f.write('李四')
    
# 读文件
with open('E:\git-clone\zhaoya-git\dev1.txt','r',encoding='utf-8') as f:
	for line in f.readlines(): # readlines 一次读取所有内容并按行返回list readline 读取一行内容
		print(line.strip())
```

## 内存读写【StringIO、BytesIO】

> `StringIO`操作字符串
>
> ```python
> from io import StringIO
> def bar():
>     f=StringIO()
>     f.write('张三')
>     print(f.getvalue())
>     
> if __name__ == "__main__":
>     bar()
> ```

> `BytesIO`操作二进制
>
> ```python
> >>> from io import BytesIO
> >>> f=BytesIO()
> >>> f.write('张三'.encode('utf-8'))
> 6
> >>> f.getvalue()
> b'\xe5\xbc\xa0\xe4\xb8\x89'
> ```

## 序列化和反序列化

> * **序列化**：从内存中变成可存储或传输的过程
>
> * **反序列化**：变量内容从序列化的对象重新读到内存里

* **Python提供`pickle`模块实现序列化**

```python
>>> import pickle
>>> d = dict(name='Bob', age=20, score=88)
# pickle.dumps()方法把任意对象序列化成一个bytes
>>> pickle.dumps(d)
# pickle.dump()直接把对象序列化后写入一个file-like Object
# 像open()函数返回的这种有个read()方法的对象，在Python中统称为file-like Object
>>> f = open('dump.txt', 'wb')
>>> pickle.dump(d, f)
>>> f.close()

# pickle.loads()方法反序列化出对象
>>> f = open('dump.txt', 'rb')
>>> d = pickle.load(f)
>>> f.close()
>>> d
{'age': 20, 'score': 88, 'name': 'Bob'}
```

## JSON

* **python 内置`json`模块**

```python
>>> import json
>>> d = dict(name='Bob', age=20, score=88)
>>> json.dumps(d) #dumps方法返回一个str
'{"age": 20, "score": 88, "name": "Bob"}'

# 通过loads()方法将json格式反序列化python对象
>>> json_str = '{"age": 20, "score": 88, "name": "Bob"}'
>>> json.loads(json_str)
{'age': 20, 'score': 88, 'name': 'Bob'}
```

* 将`class`序列化`json`格式

```python
# 在dumps()函数中传入转换函数【default】
import json

class Student(object):
    def __init__(self, name, age, score):
        self.name = name
        self.age = age
        self.score = score
# 转换函数
def student2dict(std):
    return {
        'name': std.name,
        'age': std.age,
        'score': std.score
    }

>>> print(json.dumps(s, default=student2dict))
{"age": 20, "name": "Bob", "score": 88}
# 通常每class都有__dict__属性，就是一个dict，存储实例变量
print(json.dumps(s, default=lambda obj: obj.__dict__))

# 同理，使用loads()函数反序列化，也需要一个转换函数【object_hook】
def dict2student(d):
    return Student(d['name'], d['age'], d['score'])

>>> json_str = '{"age": 20, "score": 88, "name": "Bob"}'
>>> print(json.loads(json_str, object_hook=dict2student))
```

## 多进程

* **`multiprocessing`模块是跨平台多进程模块，提供一个`Process`类来代理进程对象**

```python
from multiprocessing import Process
import os

# 子进程要执行的代码
def run_proc(name):
    print('Run child process %s (%s)...' % (name, os.getpid()))

if __name__=='__main__':
    print('Parent process %s.' % os.getpid())
    p = Process(target=run_proc, args=('test',))
    print('Child process will start.')
    p.start()
    p.join() # join()方法可以等待子进程结束后再继续往下运行，通常用于进程间的同步
    print('Child process end.')
```

* **进程池`Pool`**

```python
from multiprocessing import Pool
import os, time, random

def long_time_task(name):
    print('Run task %s (%s)...' % (name, os.getpid()))
    start = time.time()
    time.sleep(random.random() * 3)
    end = time.time()
    print('Task %s runs %0.2f seconds.' % (name, (end - start)))

if __name__=='__main__':
    print('Parent process %s.' % os.getpid())
    p = Pool(4)
    for i in range(5):
        p.apply_async(long_time_task, args=(i,))
    print('Waiting for all subprocesses done...')
    p.close()
    p.join()
    print('All subprocesses done.')
```

* **子进程，`subprocess`模块可以让我们非常方便地启动一个子进程，然后控制其输入和输出**

```python
import subprocess

print('$ nslookup www.python.org')
r = subprocess.call(['nslookup', 'www.python.org'])
print('Exit code:', r)
```

**如果子进程还需要输入，则可以通过`communicate()`方法输入：**

```python
import subprocess

print('$ nslookup')
p = subprocess.Popen(['nslookup'], stdin=subprocess.PIPE, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
output, err = p.communicate(b'set q=mx\npython.org\nexit\n')
print(output.decode('utf-8'))
print('Exit code:', p.returncode)
```

* **进程间通信，`multiprocessing`模块提供`Queue`和`Pipes`来交换数据**

**下面以`Queue`为例：**

```python
from multiprocessing import Process, Queue
import os, time, random

# 写数据进程执行的代码:
def write(q):
    print('Process to write: %s' % os.getpid())
    for value in ['A', 'B', 'C']:
        print('Put %s to queue...' % value)
        q.put(value)
        time.sleep(random.random())

# 读数据进程执行的代码:
def read(q):
    print('Process to read: %s' % os.getpid())
    while True:
        value = q.get(True)
        print('Get %s from queue.' % value)

if __name__=='__main__':
    # 父进程创建Queue，并传给各个子进程：
    q = Queue()
    pw = Process(target=write, args=(q,))
    pr = Process(target=read, args=(q,))
    # 启动子进程pw，写入:
    pw.start()
    # 启动子进程pr，读取:
    pr.start()
    # 等待pw结束:
    pw.join()
    # pr进程里是死循环，无法等待其结束，只能强行终止:
    pr.terminate()
```

## 多线程

* **Python提供`threading`模块创建多线程**

```python
import time, threading

# 新线程执行的代码:
def loop():
    print('thread %s is running...' % threading.current_thread().name)
    n = 0
    while n < 5:
        n = n + 1
        print('thread %s >>> %s' % (threading.current_thread().name, n))
        time.sleep(1)
    print('thread %s ended.' % threading.current_thread().name)

print('thread %s is running...' % threading.current_thread().name)
t = threading.Thread(target=loop, name='LoopThread')
t.start()
t.join()
print('thread %s ended.' % threading.current_thread().name)
```

