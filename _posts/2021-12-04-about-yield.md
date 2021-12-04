---
layout: post
title: "About iterator/generator"
date:   2021-12-04
tags: [python]
comments: true
author: Jerry8964
---



## 迭代器（iterator)

迭代是Python最强大的功能之一，是访问集合元素的一种方式。

迭代器是一个可以记住遍历的位置的对象。

迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束。迭代器只能往前不会后退。

迭代器有两个基本的方法：**iter()** 和 **next()**。

字符串，列表或元组对象都可用于创建迭代器：

```python
list1 = [1, 2, 3, 4]
it = iter(list1)
print(next(it))
```

同样，迭代器也可以用户`for`循环



### 创建一个迭代器

创建一个类的时候，只需要实现两个方法`__iter__()` 与`__next__()`就可以创建一个迭代器

`__iter__()`方法返回一个特殊的迭代器对象， 这个迭代器对象实现了 __next__() 方法并通过 StopIteration 异常标识迭代的完成

`__next__()`方法会返回下一个迭代器对象。

> 创建一个返回数字的迭代器，初始值为 1，逐步递增 1：
>
> ```python
> class MyNumbers:
>   def __iter__(self):
>     self.a = 1
>     return self
>  
>   def __next__(self):
>     x = self.a
>     self.a += 1
>     return x
>  
> myclass = MyNumbers()
> myiter = iter(myclass)
>  
> print(next(myiter))
> print(next(myiter))
> print(next(myiter))
> ```
>
> 执行结果 
>
> ```
> 1
> 2
> 3
> ```



### StopIteration

`StopIteration `异常用于标识迭代的完成，防止出现无限循环的情况，在 __next__() 方法中我们可以设置在完成指定循环次数后触发 StopIteration 异常来结束迭代。

> 在 5次迭代后停止执行：
>
> ```python
> class MyNumbers:
>   def __iter__(self):
>     self.a = 1
>     return self
>  
>   def __next__(self):
>     if self.a <= 5:
>       x = self.a
>       self.a += 1
>       return x
>     else:
>       raise StopIteration
>  
> myclass = MyNumbers()
> myiter = iter(myclass)
>  
> for x in myiter:
>   print(x)
> ```
>
> 执行输出结果为：
>
> ```
> 1
> 2
> 3
> 4
> 5
> ```



### others

一些迭代器生成的方法。

1. `enumerate`可以接收一个可迭代的对象（如：列表），然后返回一个带下标的可迭代对象。

   ```python
   names = ["Jerry", "Tom", "Alex", "Amadine"]
   for i, name in enumerate(names):
       print(i, name)
   ```

   

2. `product`可以接收多个可迭代对象，根据它们的笛卡儿积不断的生成结果。

   > 不使用product的方式，需要写多层循环
   >
   > ```python
   > names = ["Jerry", "Tom", "Alex", "Amadine"]
   > ages = [20, 25, 40, 41]
   > for name in names:
   >  for age in ages:
   >      if name.startswith("A") and age > 40:
   >          print(name, age)
   > ```

   使用`product`的代码

   ```python
   for name, age in product(names, ages):
       if name.startswith("A") and age > 40:
           print(name, age)
   ```



## 生成器（generator)

在 Python 中，使用了 yield 的函数被称为生成器（generator）。

跟普通函数不同的是，生成器是一个返回迭代器的函数，只能用于迭代操作，更简单点理解生成器就是一个迭代器，但是只有在使用的时候才会生成，并不是一次性全部生成好。

在调用生成器运行的过程中，每次遇到 yield 时函数会暂停并保存当前所有的运行信息，返回 yield 的值, 并在下一次执行 next() 方法时从当前位置继续运行。

调用一个生成器函数，返回的是一个迭代器对象。

以下实例使用 yield 实现斐波那契数列：

```python
#!/usr/bin/python3
 
import sys
 
def fibonacci(n): # 生成器函数 - 斐波那契
    a, b, counter = 0, 1, 0
    while True:
        if (counter > n): 
            return
        yield a
        a, b = b, a + b
        counter += 1
f = fibonacci(10) # f 是一个迭代器，由生成器返回生成
 
while True:
    try:
        print (next(f), end=" ")
    except StopIteration:
        sys.exit()
```

输出结果 

```
0 1 1 2 3 5 8 13 21 34 55
```



### yield

**在Python开发过程中，为了避免程序占用过多的内存，特别是在处理大量的数据的时候，建议多使用`yield`关键字**

* 更多的使用`yield`关键字，返回生成器对象，而不是直接返回全部值。（由于生成器（Generator）对象，是在被引用到的时候才会计算生成，所以不会大量的占用内存）

* 使用生成器表达式，代替列表表达式

  > 生成器表达式

  ```python
  (i for i in range(10))
  ```

  > 列表表达式

  ```python
  [i for i in range(10)]
  ```

* 尽量使用模块提供的懒惰对象，而不是一次性把所有需要的数据都读取出来。

  例如：

  1. 使用`re.finditer`替代`re.findall`

  2. 直接使用可迭代的文件对象

     ```python
     fp = open("temp.txt", "r")
     for line in fp:
         do_something
     ```

     而不是

     ```python
     fp = open("temp.txt", "r")
     for line in fp.readlines():
         do_something
     ```








--end--
