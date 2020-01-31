---
layout: post
title: basenameコマンドの使い方
date: 2020-01-31 23:51:04
tags: [sh,basename]
---

basenameの初めて見る使い方を見たのでメモ

# 環境

- Ubuntu18.04
  - bash

# 出来ること

パスで指定されたファイルやフォルダの名前だけを出力する

以下の様にファイルが配置されているとします。

```bash
$ mkdir test
$ cd test
$ mkdir dir1
$ touch dir1/test.sh
$ find
.
./dir1
./dir1/test.sh
```

## ファイル名を出力する

パスは要らない時などに使える。

```bash
$ basename ./dir/test.sh
test.sh
```

## ファイル名の末尾文字を削除し出力する

これで拡張子を消したりできる。

```bash
$ basename ./dir/test.sh .sh
test
```
