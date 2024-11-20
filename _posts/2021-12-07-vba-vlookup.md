---
layout: post
title: "VLOOKUP"
date: 2021-12-07
tags: [vba]
comments: true
author: Jerry8964
---



**Summary**: Usage of system function `vlookup`

## VLOOKUP

エクセル業務の際、なるべく効率的に作業したいという方も多いと思います。また、必要なデータを目視で探して手入力していては工数もかかり、ミスも起こりやすいです。

そこで、`VLOOKUP(検索値, 範囲, 返却列番号, 検索方法)`関数の使い方を説明したいと思います。

>  VLOOKUP関数とは、検索条件に一致するデータを指定範囲の中から探して表示してくれる関数です。

`VLOOKUP`が4つパラメータがあり、

> 1. 検索値：検索する値を入力します。
> 2. 範囲：上記検索値を検索する範囲を選択する。
> 3. 列番号：リターン値です、検索値を合っている場合、どの列を返却する。
> 4. 検索方法：TRUE/FALSE、TRUEは基本一致（曖昧検索できる）FALSEは完全一致。



例：

テーブルAから商品名称をテーブルBに転記したい場合。

![](https://raw.githubusercontent.com/jerry8964/jerry8964.github.io/main/images/vlookup-0001.JPG)



下記のような入力すれば、自動的にマッピングできます。

![](https://raw.githubusercontent.com/jerry8964/jerry8964.github.io/main/images/vlookup-00002.JPG)

> セルのアルファベット（列）と数字（行）の前に`$`を追加すれば、セルを固定値できます。

F3からF7まで選択し、HotKey`Ctrl + D`を押すと、書式の自動コピーができます。

![](https://raw.githubusercontent.com/jerry8964/jerry8964.github.io/main/images/vlookup-00003.JPG)





--end--