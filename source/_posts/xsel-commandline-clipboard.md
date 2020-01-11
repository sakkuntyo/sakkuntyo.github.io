---
layout: post
title: コマンドラインの出力をクリップボードにコピー
date: 2020-01-12 04:03:19
tags: [xsel,ubuntu]
---

ターミナルに出てきた文字列をコピーしたい、
ただしマウス触るのがめんどくさい。。。
そんな時に

# 環境

- Ubuntu18.04

# インストール

```bash
$ apt update
$ apt install xsel -y
```

# 使い方

## 1. 出力をクリップボードにコピー

```bash
$ echo "Hellow" | xsel --clipboard --input
```

この後右クリックやCtrl+Vで貼り付けできる様になっています。
