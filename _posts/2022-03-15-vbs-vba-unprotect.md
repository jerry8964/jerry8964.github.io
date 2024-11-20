---
layout: post
title: "VBSからVBAを呼び出すとき、「変更しようとしているセル...」エラー"
date:   2022-03-15
tags: [doc, vba]
comments: true
author: Jerry8964
---



**Summary**: When I want to call a VBA macro from a VBS, error occured...

## VBSからVBAを呼び出すとき、エラーが発生



### 背景

ExcelのVBAを作ったんですが、Windowsスケジュールで実行させたいですので、呼び出し用VBSを作りました。ただVBSからVBAを呼び出すとき、保護解除してくださいというエラーが出てきました。



### 事象

エラー内容は：変更しようとしているセルやグラフは保護されているシート上にあります。変更するには、シートの保護を解除してください。パスワードの入力が必要な場合もあります。

こちら実行する時、エラー内容がエラーログに出力したので、下記のようなメッセージボックスがありませんが、事象が同じです。

![](https://github.com/jerry8964/jerry8964.github.io/blob/main/images/excel-error-this-sheet-protected-error.png?raw=true)

Debugで原因特定したところ、Excel画面のコンボボックスを値に設定しようとしたとき、エラーが発生しました。

ソースは大体下記となります。

```vba
ActiveSheet.Unprotect
cmb_Combobox.value = "設定したい値"
ActiveSheet.protect
```

ソースを見ると、値設定前にすでに保護を解除しました。エラー原因特定できませんでした。



※画面から直接実行する時、該当エラーが発生されません。VBSから呼び出しの時のみ発生します。

### 対応

考えとしては、VBSから呼び出すとき、ActiveSheetコマンドでシートの特定できない可能性があります。

下記修正で対応してみましたが、直しませんでした。

```vba
ThisWorkbook.Sheet("SheetName").Unprotect
cmb_Combobox.value = "設定したい値"
ThisWorkbook.Sheet("SheetName").protect
```

VBSから実行すると、同じエラーが発生しました。



Withブロックが一番強いと思いますので、下記ソースで試しました。具体的な原因わかりませんが、解決できました。

```vba
With ThisWorkbook.Sheet("SheetName").Unprotect
    cmb_Combobox.value = "設定したい値"
End With
```



### 原因

とりあえず原因不明です。



