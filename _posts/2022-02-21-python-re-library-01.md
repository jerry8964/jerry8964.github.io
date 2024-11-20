---
layout: post
title: "Python re library"
date:   2022-02-21
tags: [doc, python]
comments: true
author: Jerry8964
---







Summary: re library of Python. from website but I transate some of them for reference.

## 简单说明

re库是Python的一个内置模块，使用的时候直接引用即可。

> Both patterns and strings to be searched can be Unicode strings ([`str`](https://docs.python.org/3/library/stdtypes.html#str)) as well as 8-bit strings ([`bytes`](https://docs.python.org/3/library/stdtypes.html#bytes)).

模式（查找的条件，对应下面的pattern参数）和被搜索的字符串（搜索目标）即可以是Unicode（即人可以阅读的字符串）也可以是8bit（bytes）的string（即转译为二进制的字符内容）。

> However, Unicode strings and 8-bit strings cannot be mixed: that is, you cannot match a Unicode string with a byte pattern or vice-versa; similarly, when asking for a substitution, the replacement string must be of the same type as both the pattern and the search string.

但是Unicode和bytes不能混用：也就是说，不能用字节串模式匹配 Unicode 字符串，反之亦然；同理，替换操作时，替换字符串的类型也必须与所用的模式和搜索字符串的类型一致。



> It is important to note that most regular expression operations are available as module-level functions and methods on [compiled regular expressions](https://docs.python.org/3/library/re.html#re-objects). The functions are shortcuts that don’t require you to compile a regex object first, but miss some fine-tuning parameters.

值得提醒的一点是，基本上所有的函数都支持直接的正则表达式和编译后的正则表达式，不需要事先编译就可以使用这算是一个捷径，当然，这会损失了一些优先的参数。



## 函数详解

### compile函数

将正则表达式**编译成一个Pattern对象**。Pattern对象可以调用上述函数的同名函数实现对应的功能，事实上，在上述函数的底层，也是先通过传入的pattern和flags函数编译出对应的Pattern对象，再调用Pattern对象的相应函数的。

```python
def compile(pattern, flags=0) #函数接口
```

示例如下。

```python
>>> pattern = re.compile('\d{2}')
>>> pattern.match('09计算机71软件工程91人工智能')
<re.Match object; span=(0, 2), match='09'>
```

### match函数：

从字符串的开头进行匹配，返回一个Match对象，失败则返回空对象。

```python
def match(pattern, string, flags=0) #函数接口
```

示例如下，match是从字符串开头开始进行匹配的，第一个命令成功的匹配了目标字符串中的09，而第二个命令中，尽管目标字符串中有计算机，但因为它不在字符串的开头，所以依然匹配失败。如果希望取消从头开始的限制，我们需要借助search函数解决。

```python
>>>re.match('\d{2}','09计算机71软件工程')
<re.Match object; span=(0, 2), match='09'>
>>>re.match('计算机','09计算机71软件工程')
```

### fullmatch函数

匹配**整个字符串**，返回一个Match对象，如果匹配失败则返回空对象

```python
def fullmatch(pattern, string, flags=0) #函数接口
```

示例如下，可以发现fullmatch是针对目标字符串整体而言进行匹配的。

```python
>>> re.fullmatch('\d*软件','71软件工程')
>>> re.fullmatch('\d*软件工程','71软件工程')
<re.Match object; span=(0, 6), match='71软件工程'>
```

### search函数

在字符串中**搜索与pattern匹配的部分**，返回一个Match对象，如果匹配失败则返回空对象

```python
def search(pattern, string, flags=0) #函数接口
```

示例如下，可以发现search不再受到match中的限制，它将从左到右、在整个字符串中搜索与pattern匹配的部分，直到**找到第一个匹配时停止**。

```python
>>> re.search('\d{2}','09计算机71软件工程')
<re.Match object; span=(0, 2), match='09'>
>>> re.search('计算机','09计算机71软件工程')
<re.Match object; span=(2, 5), match='计算机'>
>>> re.search('人工智能','09计算机71软件工程')
```

### sub函数

在目标字符串中搜索到**匹配pattern的部分(包括接下来的函数同样适用的一点，这种匹配的部分彼此之间并不重叠)，并将它替换为repl，返回替换后的字符串**。 如果**匹配失败，则原封不动的返回string**。repl可以是**字符串或是回调函数**；如果它是字符串，则其中任何反斜杠转义序列都会被处理，像\n就会被转换为换行符。默认状态(count=0)的情况下我们会将所有符合pattern的部分都替换，如果希望只替换部分，可以通过count控制次数

```python
def sub(pattern, repl, string, count=0, flags=0) #函数接口
```

示例如下。

```python
>>> re.sub('\d{2}','_','09计算机71软件工程91人工智能')
'_计算机_软件工程_人工智能'
>>> re.sub('\d{3}','_','09计算机71软件工程91人工智能')
'09计算机71软件工程91人工智能'
>>> re.sub('\d{2}','_','09计算机71软件工程91人工智能',1)
'_计算机71软件工程91人工智能'
>>> re.sub('\d{2}','_','09计算机71软件工程91人工智能',2)
'_计算机_软件工程91人工智能'
```

如果repl是一个函数，则它应该接受一个Match对象作为参数，并且返回一个用于替换的字符串，这种情况下可以对匹配后的内容进行进一步的分类处理。

```python
>>> def my_repl(matchobj):
...     if matchobj.group(0) == '09': return 'CS'
...     elif matchobj.group(0) == '71': return 'SE'
...     elif matchobj.group(0) == '91': return 'AI'
...
>>> re.sub('\d{2}',my_repl,'09计算机71软件工程91人工智能')
'CS计算机SE软件工程AI人工智能'
```

### subn函数

返回**(’字符串‘，替换次数)的二元组**，其它的用法和上述sub函数一致

```python
def subn(pattern, repl, string, count=0, flags=0) #函数接口
```

示例如下。

```python
>>> re.subn('\d{2}','_','09计算机71软件工程91人工智能')
('_计算机_软件工程_人工智能', 3)
>>> re.subn('\d{2}','_','09计算机71软件工程91人工智能',2)
('_计算机_软件工程91人工智能', 2)
>>> re.subn('\d{3}','_','09计算机71软件工程91人工智能',2)
('09计算机71软件工程91人工智能', 0)
```

### split函数

将目标字符串以**匹配pattern的部分作为隔板进行分隔，返回一个子字符串的列表**。如果**正则表达式采用了捕获组的形式，那么匹配pattern的部分也会被放入结果列表**。默认状态(maxsplit=0)的情况下我们会分割整个目标字符串，在指定maxsplit的情况下，我们在前maxsplit个隔板的位置做字符串分割，而把最后的剩余部分作为一个完整的字串返回

```python
def split(pattern, string, maxsplit=0, flags=0) #函数接口
```

示例如下，要注意**如果匹配到字符串的开始，那么结果会以一个空字符串开始**。这点对于匹配到结尾的情况也是同理。

```python
>>> re.split('\d{2}','09计算机71软件工程91人工智能')
['', '计算机', '软件工程', '人工智能']
>>> re.split('(\d{2})','09计算机71软件工程91人工智能')
['', '09', '计算机', '71', '软件工程', '91', '人工智能']
>>> re.split('(\d{2})','09计算机71软件工程91人工智能',2)
['', '09', '计算机', '71', '软件工程91人工智能']
```

### findall函数

以**列表的形式返回目标字符串中与pattern匹配的部分**，如果正则表达式中含有一个或多个捕获组，则会返回一个捕获组列表

```python
def findall(pattern, string, flags=0) #函数接口
```

示例如下，我们发现在正则表达式中含有两个捕获组时，该函数也返回对应顺序的二元组。而当匹配失败时，函数会返回一个空列表。

```python
>>> re.findall('\d{2}','09计算机71软件工程91人工智能')
['09', '71', '91']
>>> re.findall('(\d{2})([a-z]{2})','09aa计算机71bb软件工程91cc人工智能')
[('09', 'aa'), ('71', 'bb'), ('91', 'cc')]
>>> re.findall('\d{3}','09计算机71软件工程91人工智能')
[]
```

### finditer函数

返回一个**表示字符串中与pattern匹配部分的可迭代对象**，可迭代对象中的每一个元素都是一个对应的Match对象

```python
def finditer(pattern, string, flags=0) #函数接口
```

示例如下，我们通过该函数对目标字符串实现了一个遍历。

```python
>>> re.finditer('\d{2}','09计算机71软件工程91人工智能')
<callable_iterator object at 0x00000182DFE37D88>
>>> result = re.finditer('\d{2}','09计算机71软件工程91人工智能')
>>> for i in result:
...     print(i.group())
...
09
71
91
```





--遇到新的内容会存时补充--