---
layout: post
title: "FileSystemObjectについて"
date: 2021-09-01
tags: [vba]
comments: true
author: Jerry8964
---



**Summary**

> 因为VBA的FileSystemObject.GetFolder.Files返回的是一个迭代对象，所以如果对当前文件夹下面的文件有操作的话会被视为新的文件，而增加到返回的队列里。



VBAのFileSystemObjectを使うとき、下記のような指定されたフォルダしたのファイルを全部リストアップすることができる。

```vbscript
FileSystemObject.GetFolder("full_path").Files
```

しかも、`GetFolder.Files`のリターン値はIteratorと呼ぶされるものであり、

プログラムの処理時間帯に、対象フォルダしたに新規ファイルがあれば、新規したファイルも処理対象になりますので、使用する時、注意しないとバグが発生かもしれない。

例えば：

> 取得したファイルをループし
>
> 毎回処理完了したら、新規ファイルとして、同じフォルダに保存する場合、
>
> バグが発生される

ソース

```vbscript
Dim file
Dim fso as FileSystemObject
For Each file in fso.GetFolder("full_path").Files
    new_file = file & "_"
    Name file as new_file
    set ObjectText = fso.CreateTextFile(file.true)
    ObjectText.Write "your content"
    fso.DeleteFile new_file
file.Next
```

> ソースに、取得されたファイルの内容を処理し、処理した内容を新規ファイルに登録した後
>
> 新規ファイルを元ファイルの名前に変更する。
>
> .Filesとして、ファイル名が同じですが、同じファイルではないとするので、
>
> fso.GetFolder.countが増える。バグが起きる



> Source里将原文件的内容处理之后写入到新文件，并重新命名回原来的文件名，但是对于Files来说新的文件并不是原来的那个文件了，这个时候fso.GetFolder.count也会增加。会产生Bug。



--end--

