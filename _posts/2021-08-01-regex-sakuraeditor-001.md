---
layout: post
title:  "仕事便利帳(固定)"
date: 2024-06-05:w
tags: [doc, regex, linux]
comments: true
pinned: true
toc: false
author: Jerry8964
---





Summary：正規表現で指定した文字含めていない行の検索、フォルダやファイル名の一括置き換え、ファイル更新日付により指定フォルダに移動。

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



### ファイルの更新日付によって指定フォルダ下に移動する

> B-shell

**指定日付のみのファイル操作したいなら**

```bash
mkdir -p 202405 && find . -maxdepth 1 -type f -newermt 2024-05-01 ! -newermt 2024-06-01 -exec mv "{}" 202405/ \;
```



**すべてのファイルを処理したい場合**

```bash
#!/bin/bash

# Loop through all files in the current directory
for file in *; do
  if [ -f "$file" ]; then
    # Get the last modified date of the file in YYYYMMDD format
    mod_date=$(date -r "$file" +"%Y%m%d")
    
    # Create the directory if it doesn't exist
    mkdir -p "$mod_date"
    
    # Move the file to the directory
    mv "$file" "$mod_date/"
  fi
done

# If you dont want to zip the folder , just move the line below.
# Loop through all directories in the current directory
for dir in */; do
  # Remove the trailing slash
  dir=${dir%/}
  
  # Zip the directory
  zip -r "$dir.zip" "$dir"
  
  # Optionally, remove the directory after zipping
  rm -rf "$dir"
done

```

・実行権限を付与する

```bash
chmod +x move_files_by_date.sh
```

・実行する

```bash
./move_files_by_date.sh
```





