---
layout: post
title: "Salesforce Learning Note"
date: 2021-12-13
tags: [salesforce, japanese]
comments: true
author: Jerry8964
---





## 第一回

### About `Sales life cycle`

<img src="https://raw.githubusercontent.com/jerry8964/jerry8964.github.io/main/images/20211213203635.png" style="zoom:80%;" />

### Salesforce認定資格一覧

[認定資格一覧](https://tandc.salesforce.com/credentials)

[資格取得のコースフロー](https://www.trainocate.co.jp/reference/flow/71-2.html)



**権限**

Salesforceのテーブルにアクセスする権限はprofileに付いている、profileを持っている方はテーブルのアクセス権限が同じです。

> 同じテーブルにアクセスできますが、見られるデータが別の方法でコントロールできます。詳しい第二回の権限部分をご参照ください。





## 第二回



**雑談**

> SFDCにベースして作ったプログラム：[Veeva](https://www.veeva.com/jp/resources/)
>
> 個人的にSFDCにベースしてプログラムを作って、`appexchange`にアップロードすれば
>
> 他の方に見せることができます。



### 権限

RBAC：Role-Based Access Control

前にProfileも紹介していたのが、RoleとProfileはどの違うがありますか。

<img src="https://raw.githubusercontent.com/jerry8964/jerry8964.github.io/main/images/20211213210934.png" style="zoom:67%;" />

Profile：テーブルのAccess権限をコントロールする

Role：テーブルのデータの見える見えない権限をコントロールする

例えば、上の図にFrontチームとEndチームが接続できるテーブルが違い、同じチームに部長と社員は同じテーブルに接続できますが、見られるデータ内容が違います。

`setup` 　→　`profiles` 

`setup`　→　`roles`

具体的な権限コントロール例は、下記例をご覧ください。

<img src="https://raw.githubusercontent.com/jerry8964/jerry8964.github.io/main/images/20211213212543.png" style="zoom:67%;" />



