---
layout: post
title: "Use Input Dialog create a dropdown list in UiPath"
date:   2024-01-05
tags: [UiPath]
comments: false
author: Jerry8964
---



**Summary**: How to create a dropdown list in UiPath.

## 背景

最近接触到`UiPath`，需要创建 个让用户选择的下接列表（Dropdown List)，在网上查询了很多关于如何创建下拉列表的示例。但是基本上都是通过`Create Form Task`这个`Activity`来实现的。

在与现场的`UiPath`前辈咨询之后，对方表示用`Input Dialog`就可以简单的实现一个下拉列表。

下面是关于如何实现的一个示例。



## 示例

1. 首先在你的`Workflow`或`Sequence`里增加一个`Input Dialog`的`Activity`
2. `Input Type`设置成`Multiple Choice` （这里表示会有多个选项，默认的`Text Box`则会直接产生一个输入框要求用户输入）
3. `Dialog Tile`中输入你希望表示的对话框的标题，注意使用双引号括起来。
4. `Input Label`里面输入你想展示给用户的内容，比如”请在下拉列表中选择您想执行的对象。“，不想展示任何内容则留空。
5. `Input options`里面输入你的备选项，以半角分号`;`进行分割。
   如："选项1;选项2;选项3;选项4"
   在这里需要注意的是，如果给出的选项低于**4**个的话，则会以单选`Radio box`的方式展示，大于4个则会自动切换为下拉列表来展示。
6. `Value entered`里面，按`Ctrl + K`输入你想定义的变量名称则可以将用户的选择内容保存到变量里。



## 执行结果 



**Input Type设置成Text Box时**





**3个及以下选项时**





**4个或者以上的选项时**





## 总结 

当只需要一个`Dropdown List`的时候，通过`Input Dialog`的确可以实现，但是需要生成多个`Dropdown List`的时候，则必须通过网上介绍的`Create Form Task`的`Activity`来实现了。具体的可以参照网上的一些介绍，这样的例子很容易找到。
