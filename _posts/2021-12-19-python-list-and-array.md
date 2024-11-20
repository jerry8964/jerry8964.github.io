---
layout: post
title: "List and Array of Python"
date: 2021-12-19
tags: [python, learning]
comments: true
author: Jerry8964
---


**Summary**: List and arrary of python, difference and which one to use?

虽然列表（list）既灵活又简单，但面对各类需求时，我们可能会有更好的选择。比如，要存放1000万个浮点数的话，数组（array）的效率要高得多，因为数组在背后存的并不是`float`对象，而是数字的机器翻译，也就是字节表述。这一点就跟C语言中的数组一样。再比如说，如果需要频率对序列做先进先出（FIFO）的操作，双端队列（deque）的速度应该会更快。

如果要检查一个元素是否在某个集合中，用`set`会更合适。set专为检查元素是否存在做过优化，但它并不是序列，因为set是无序的。



如果我们需要一个只包含数字的列表，那么`array.array`比`list`更高效。数组支持所有跟可变序列有关的操作，包括`.pop`，`.insert`和`.extend`。另外，数组还提供从文件读取和存入文件的更快的方法，如`.frombytes`和`.tofile`

Python的数组跟C语言数组一样精简。创建数组需要一个类型码，这个类型码用来表示在底层的C语言应该存放怎样的数据类型。比如b类型码代表的是有符号的字符(signed char)，因此`array('b')`创建出的数组就只能存放一个字节大小的整数，范围从-128到127，这样在序列很大的时候，我们能节省很多空间。而且Python不会允许你在数组里存放除指定类型之外的数据。

例：

```python	
from array import array
from random import random
floats = array('d', (random() for i in range(10**7)))
# 查看数组的最后一个元素
print(floats[-1])
fp = open('floats.bin', 'wb')
# 把数组存入一个二进制文件
floats.tofile(fp)
fp.close()
# 新建一个双精度浮点空数组
floats2 = array('d')
fp = open('floats.bin', 'rb')
# 把1000万个浮点数从二进制文件里读取出来
floats2.fromfile(fp, 10**7)
fp.close()
# 查看最后一个元素
print(floats2[-1])
# 检查两个数组的内容是否完全一致（结果为True）
print(floats2 == floats)
```

> 结论：array.tofile和array.fromfile用起来很简单，而且很快。



下面总结一下列表`list`和数组`array`的一些功能。

| 功能                      | 列表 | 数组 | 说明                                                         |
| :------------------------ | ---- | ---- | ------------------------------------------------------------ |
| `s.__add__(s2)`           | 〇   | 〇   | 拼接s + s2                                                   |
| `s.__iadd__(s2)`          | 〇   | 〇   | 就地拼接 s += s2                                             |
| `s.append(e)`             | 〇   | 〇   | 在尾部添加一个元素                                           |
| `s.byteswap`              |      | 〇   | 翻转数组内的每个元素的字节序列，转换字节序                   |
| `s.clear()`               | 〇   |      | 删除所有元素                                                 |
| `s.__contains__(e)`       | 〇   | 〇   | s是否含有e                                                   |
| `s.copy()`                | 〇   |      | 对列表浅复制                                                 |
| `s.__copy__()`            |      | 〇   | 对copy.copy的支持                                            |
| `s.count(e)`              | 〇   | 〇   | s中e的出现次数                                               |
| `s.__deepcopy__()`        |      | 〇   | 对copy.deepcopy的支持                                        |
| `s.__delitem__(p)`        | 〇   | 〇   | 删除位置p的元素                                              |
| `s.extend(it)`            | 〇   | 〇   | 将可迭代对象it里的元素添加到尾部                             |
| `s.frombytes(b)`          |      | 〇   | 将压缩成机器值的字节序列读出来添加到尾部                     |
| `s.fromfile(f, n)`        |      | 〇   | 将二进制文件f内含有机器值读出来添加到尾部，最多添加n项       |
| `s.fromlist(l)`           |      | 〇   | 将列表里的元素添加到尾部，如果其中任何一个元素导致了TypeError异常，那么所有的添加都会被取消 |
| `s.__getitem__(p)`        | 〇   | 〇   | s[p], 读取位置p的元素                                        |
| `s.index(e)`              | 〇   | 〇   | 找到e在序列中第一次出现的位置                                |
| `s.insert(p, e)`          | 〇   | 〇   | 在位于p的元素之前插入元素e                                   |
| `s.itemsize`              |      | 〇   | 数组中每个元素的长度是几个字节                               |
| `s.__iter__()`            | 〇   | 〇   | 返回迭代器                                                   |
| `s.__len__()`             | 〇   | 〇   | len(s)，序列的长度                                           |
| `s.__mul__(n)`            | 〇   | 〇   | s * n，重复拼接                                              |
| `s.__imul__(n)`           | 〇   | 〇   | s *= n， 就地重复拼接                                        |
| `s.__rmul__(n)`           | 〇   | 〇   | n * s， 反向重复拼接                                         |
| `s.pop([p])`              | 〇   | 〇   | 删除位于p的值并返回这个值，默认删除最后一个元素。            |
| `s.remove(e)`             | 〇   | 〇   | 删除序列里第一次出现的e元素                                  |
| `s.reverse()`             | 〇   | 〇   | 就地调转序列中元素的位置                                     |
| `s.__reversed__()`        | 〇   |      | 返回一个从尾部开始扫描元素的迭代器                           |
| `s.__setitem__(p, e)`     | 〇   | 〇   | s[p] = e， 把位于p位置的元素替换成e                          |
| `s.sort([key], [revers])` | 〇   |      | 就地排序序列，可选参数有key和reverse                         |
| `s.tobytes()`             |      | 〇   | 把所有元素的机器值用bytes对象的形式返回                      |
| `s.tofile(f)`             |      | 〇   | 把所有元素以机器值的形式写入一个文件                         |
| `s.tolist()`              |      | 〇   | 把数组转换成列表， 列表里的元素类型是数字对象                |
| `s.typecode`              |      | 〇   | 返回只有一个字符的字符串，代表数组元素在C语言中的类型        |



从Python3.4开始，数组`array`类型不再支持诸如`list.sort()`这种就地排序的方法。要给数组排序的话，需要用`sorted`函数新建一个数组：

`a = array.array(a.typecode, sorted(a))`

想要在不打乱次序的情况下为数组添加新的元素，`bisect.insort`还是可以使用。

如果经常使用数组，那不得不提一下`memoryview`, memoryview是一个内置的类，它能让用户在不复制内容的情况下操作同一个数组的不同切片。memoryview的概念受到了`NumPy`的启发。

详细可以参数官方文档[https://docs.python.org/zh-cn/3/c-api/memoryview.html](https://docs.python.org/zh-cn/3/c-api/memoryview.html)



--end--