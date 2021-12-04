---
layout:post
title: "Empty/NULL/Nothing/空字符串/vbNullString"
date: 2021-09-02
tags: [vba]
comments: true
author: Jerry8964
---



在VBA的编写中，经常需要给变量赋值 ，那么Empty，Null，Nothing，空字符串与vbNullString的区别是什么呢。

### Empty

一般是指空白的Cell值

或者

变体类型未初始化的时候的值 



### Null

变体类型未初始化的时候为Empty不为Null，但可以把变体类型设置为Null表示值不存在。例如从DB里面取值的时候。



### Nothing

Nothing是Object类型的对象的初期值

当一个Object变量未被指向任何实例化的Instance的时候，则会Nothing



### 空字符串（“”）

String类型的变量，未初始化的时候为空字符串



### vbNullString

基本上与空字符串相同，如果判断String有没有被赋值可以`StrPtr()`即使被赋为`""`StrPtr也会返回`True`

> **StrPtr**
>
> 用来返回字符串的缓冲区地址，当取到的字符串为空（包含Null与“”）的时候会返回0，即True

使用方法参见

[https://satokaede-sampo.com/program/post-246/](https://satokaede-sampo.com/program/post-246/)



--end--
