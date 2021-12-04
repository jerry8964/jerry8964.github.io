---
layout: post
title: "About yield"
date:   2021-12-04
tags: [Doc, Content]
comments: true
author: Jerry8964
---

**在Python开发过程中，为了避免程序占用过多的内存，特别是在处理大量的数据的时候，建议多使用`yield`关键字**

* 更多的使用`yield`关键字，反正生成器对象，而不是直接返回列表。（由于生成器（Generator）对象，是在被引用到的时候才会计算生成，所以不会大量的占用内存）

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


---

下面内容是否能避免大量的使用内存，未经验证，暂且记录下来。

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
   >     for age in ages:
   >         if name.startswith("A") and age > 40:
   >             print(name, age)
   > ```

   使用`product`的代码

   ```python
   for name, age in product(names, ages):
       if name.startswith("A") and age > 40:
           print(name, age)
   ```




--end--
