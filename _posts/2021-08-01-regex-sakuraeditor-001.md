---
layout: post
title:  "仕事便利帳"
date: 2021-08-01
tags: [doc, regex, linux]
comments: true
pinned: true
toc: false
author: Jerry8964
---



### 指定した文字列を含めてない行の検索

> **regex**

サクラエディタで指定された文字列を含めっていない行を検索したい場合、下記正規表現を使えば。

```
^((?!指定した文字列).)*$
```

> 在SakuraEditor里面搜索不包含指定字符的行的时候，可以使用上面的正规匹配。



### フォルダやファイル名の一括置換

#### ファイル

> **B-shell**

```shell
for name in *.sql
do
mv $name ${name//searchString/replaceString}
done
```

> **Powershell**

```powershell
ls *.csv | Rename-Item -NewName {$_.name -replace "searchString","replaceString"}
```

#### フォルダ

> **B-shell**

```shell
for name in `ls |sed "s/\///"`
do
mv $name ${name//searchString/replaceString}
done
```



