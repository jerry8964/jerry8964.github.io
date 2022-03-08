---
layout: post
title: "SQLのJoinについて"
date:   2022-03-08
tags: [doc, database]
comments: true
author: Jerry8964
---



## SQLサーバーのJoin



### Left, Right, Inner, Outer Joinについて

下記１図でLeft Join, Right Join, Inner Join, Outer Joinの理解ができます。

*Where条件によって、青い部分の変化がありますので、ご注意ください。*

![image-20220308203230310](https://github.com/jerry8964/jerry8964.github.io/blob/main/images/image-20220308203230310.png?raw=true)



### Cross Joinについて

Cross Joinは前の結合方法と違って、ONでマッチ条件を指定しません。

「左テーブル」 CROSS JOIN 「右テーブル」 のように結合すると、「左テーブル」 と 「右テーブル」の両方のテーブルの、全ての<ruby>コンビネーション<rp>(</rp><rt>combination</rt><rp>)</rp></ruby>の行の結果セットを取得することができます。

ですので、結果で得られるレコード数は [ 左のテーブルのレコード数 ] x [ 右のテーブルのレコード数 ] になります。

下記図はCross Joinのイメージです。

<img src="https://github.com/jerry8964/jerry8964.github.io/blob/main/images/Cross-Join-Two-Tables-to-Get-Combinations.png?raw=true" style="zoom: 67%;" />



## Joinの<ruby>アルゴリズム<rp>(/rp><rt>algorithm</rt><rp>)</rp></ruby>

Joinのアルゴリズムは3種類があり、SQL-ServerとOracleは同じ3種類全部サポートされています。MySQLはNested Loop Joinのみだそうです。

これから3種類のJoinのアルゴリズムの違いを説明します。

### Loop Join 

> 方の結合入力が少なく (たとえば 10 行未満)、他方の結合入力が多く、その結合列にインデックスが設定されている場合、インデックスの入れ子になったループが最も高速な結合演算です。入れ子になったループは I/O が最も少なく、比較が最も少なくなるためです。[^1]



下記動画のイメージです[^2]。

![loop join](https://github.com/jerry8964/jerry8964.github.io/blob/main/images/Nested-Loop-Join-50fps-1.gif?raw=true)



### Merge Join

> 2 つの結合入力が少なくない場合でも、結合列に基づいて並べ替えられている場合 (並べ替えられたインデックスのスキャンにより取得された場合など)、マージ結合が最も高速な結合演算です。 両方の結合入力が多く、2 つの入力が同じようなサイズの場合、あらかじめ並べ替えられたマージ結合とハッシュ結合は同じようなパフォーマンスになります。 ただし、2 つの入力サイズが大きく異なる場合、ハッシュ結合演算の方がはるかに高速になることが多くなります。[^1]



下記動画のイメージです。[^2]

![merge join](https://github.com/jerry8964/jerry8964.github.io/blob/main/images/Merge-Join-1.gif?raw=true)

### Hash Join

> ハッシュ結合は、並べ替えられておらず、インデックスが設定されていない大量の入力を効率的に処理できます。 次のような理由から、ハッシュ結合は、複雑なクエリでの中間結果を得るのに役立ちます。
>
> - 中間結果にはインデックスが設定されず (ディスクに明示的に保存した後インデックスを設定しない限り)、多くの場合、クエリ プランでの次の演算に合わせて並べ替えられることがありません。
> - クエリ オプティマイザーは、中間結果のサイズだけを予想します。 複雑なクエリではこの予想が非常に不正確になる場合があります。そのため、中間結果を処理するアルゴリズムは効率的なだけでなく、中間結果が予想をはるかに上回る場合でも、パフォーマンスをあまり低下させないようにする必要があります。
>
> ハッシュ結合では、非正規化の使用を減らすことができます。 通常、非正規化は、結合演算を減らすことにより、パフォーマンスを向上させるときに使用します。ただし、不整合な更新など、データの冗長性が発生するおそれがあります。 ハッシュ結合では、非正規化の必要性が減少します。 ハッシュ結合では、列方向のパーティション分割 (単一テーブルの列グループを異なるファイルまたはインデックスに格納することを表します) を物理データベース デザインに利用できます。[^1]



下記動画のイメージです。[^2]

![Hash join](https://github.com/jerry8964/jerry8964.github.io/blob/main/images/Hash-Match-Join-Looping-1.gif?raw=true)

## その他



---to be continue



[^1]:Microsoft Documentation
[^2]:写真や動画などネットから調べたのです。