---
layout: post
title:  "仕事便利帳"
date: 2021-08-01
tags: [doc, regex, linux]
comments: true
toc: false
author: Jerry8964
---





### 指定した文字列を含めていない行の検索

**`regex`**

サクラエディタで指定された文字列を含めっていない行を

検索したい場合、下記正規表現を使えば。

```
^((?!指定した文字列).)*$
```

> 在SakuraEditor里面搜索不包含指定字符的行的时候，可以使用上面的正规匹配。



### 指定されたフォルダのファイル名の変更

**`shell`**

B-Shellが使えば下記方法で簡単にファイル名の変更ができる

```shell
for name in *.sql
do
mv $name ${name//searchString/replaceString}
done
```

PowerShellなら、下記のやり方となる

```powershell
ls *.csv | Rename-Item -NewName {$_.name -replace "searchString","replaceString"}
```





--To be continue--

