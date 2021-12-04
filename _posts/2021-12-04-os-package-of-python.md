---
layout: post
title: "os package"
date: 2021-12-04
tags: [python]
comments: true
author: Jerry8964
---



在Python开发的时候，可能会需要获取主机的一些信息，这里就将通过`os`package可以获取的主机信息罗列一下，在使用过程中如果有新的内容也会及时更新。

**获取登录的用户名**

```python
os.environ.get("username")
```

**获取主机的环境变量**

```python	
os.environ["python_path"]
```

> 除了获取主机的环境变量以外，也可以设置当前program使用的主机变量，例如

```python	
os.environ["python_home"] = "C:\Users\your_python_path"
```



更多的关于`os`使用方法的内容，可以参照下面官方文档：

[https://docs.python.org/zh-cn/3/library/os.html ](https://docs.python.org/zh-cn/3/library/os.html "多种操作系统接口")



--end--
