---
layout: post
title:  "仕事便利帳"
date: 2021-08-01
tags: [doc, regex, linux]
comments: true
toc: false
author: Jerry8964
---



<detail><summary>指定した文字列を含めてない行の検索</summary>

<p>

**regex**

サクラエディタで指定された文字列を含めっていない行を

検索したい場合、下記正規表現を使えば。

```
^((?!指定した文字列).)*$
```

> 在SakuraEditor里面搜索不包含指定字符的行的时候，可以使用上面的正规匹配。

</p>

</detail>



<detail><summary>フォルダやファイル名の一括置換</summary>

<p>

#### ファイル

**shell**

B-Shellが使えば下記方法で簡単にファイル名の変更ができる

```shell
for name in *.sql
do
mv $name ${name//searchString/replaceString}
done
```

**powershell**

```powershell
ls *.csv | Rename-Item -NewName {$_.name -replace "searchString","replaceString"}
```

#### フォルダ

**shell**

```shell
for name in `ls |sed "s/\///"`
do
mv $name ${name//searchString/replaceString}
done
```

</p>

</detail>

--To be continue--

