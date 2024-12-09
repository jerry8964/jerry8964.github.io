---
layout: post
title: "VBA 32bit→64bit変更の対応パターン"
date:   2022-09-22
tags: [VBA]
comments: false
author: Jerry8964
---



**Summary**: 移植プロジェクトを対応する際に元々32bitのツールは64bit端末で運用になるため、下記対応を行いました。



## 1. データタイプの変更

### 1.1 計算するための：LongLong→ Long

変更前（64bitExcelでコンパイル場合エラーが出る）

```vba
Set rs = Nothing
' プロシージャの実行
Set rs = EDINET書類作成スケジュール_メール宛先_取得（"1", "0")
For i = 0 To rs.recordCount - 1
    s宛先 = s宛先 & rs.Fields(0).Value & ";"
    rs.MoveNext
Next
```

変更後（データタイプの変更を追加した）

```vba
Set rs = Nothing
' プロシージャの実行
Set rs = EDINET書類作成スケジュール_メール宛先_取得（"1", "0")
For i = 0 To CLng(rs.recordCount) - 1      'CLngの変更を追加する
    s宛先 = s宛先 & rs.Fields(0).Value & ";"
    rs.MoveNext
Next
```



## 2. comdlg32.dllの使用

外部から`DLL`ファイルを参照する際に、32bitバージョンと64bitバージョンの定義方法が違います。

32bitの場合

```VBA
Public Declare Function GetOpenFileName Lib "comdlg32.dll" Alias _ 
                       "GetOpenFileNameA"(pOpenFileName as OPENFILENAME) as Long
' pOpenFileName構造体（ユーザー定義型）の宣言
Type OPENFILENAME
    lStructSize    As Long    '構造体サイズ
    hwndOwner      As Long    'ダイアログを所有するウインドウハンドル
    
    hInstance      As Long
    lpstrFilter    As String
    lpstrCustomFilter  As Long
    nMaxCustrFilter   As Long
    ...
End Type
                                   
```



64bitの場合

```VBA
Public Declare PtrSafe Function GetOpenFileName Lib "comdlg32.dll" Alias _ 
                       "GetOpenFileNameA"(pOpenFileName as OPENFILENAME) as LongPtr
' pOpenFileName構造体（ユーザー定義型）の宣言
Type OPENFILENAME
    lStructSize    As Long    '構造体サイズ
    hwndOwner      As LongPtr    'ダイアログを所有するウインドウハンドル
    
    hInstance      As LongPtr
    lpstrFilter    As String
    lpstrCustomFilter  As Long
    nMaxCustFilter   As Long
    ...
End Type
```

変更内容：

1. 関すの宣言`PtrSafe`を付ける
2. Long型で参照型パラメータとなっている部分を`LongPtr`に変更する
3. 構造体のプロパティの名前変更`nMaxCustrFilter`→`nMaxCustFilter`　※詳しく上記内容を比較して確認ください。



## 3. 出力ファイルの拡張子の変更

Excelマクロの機能によってファイル生成がある場合、出力ファイルの拡張子の変更も対応する必要がある。

変更前

```VBA
' 出力ファイル名取得
strFileName = "追加・解約集計表_" & strFundCd & ".xls"
```

変更後

```VBA
' 出力ファイル名取得
strFileName = "追加・解約集計表_" & strFundCd & ".xlsm"
```

Excelブック保存処理も`xlsm`に変更する。

＜略＞





