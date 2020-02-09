---
layout: post
title: ターミナル上でパフォーマンスを確認
date: 2020-02-06 00:43:27
tags: [nmon]
---

# 環境

- Ubuntu 18.04

# インストール

```bash
$ apt update
$ apt install nmon -y
```

# 使い方

## 起動

```bash
$ nmon
```

![nmon](/images/nmon.png)

## 各パフォーマンスを確認する

各操作はコマンドで行います。

### CPU

C

![nmon1](/images/nmon1.png)

### メモリ

M

![nmon2](/images/nmon2.png)

### DISK I/O

D

### プロセス

t

![nmon3](/images/nmon3.png)

### ネットワーク

n

![nmon4](/images/nmon4.png)

### システムリソースビュー

r

![nmon5](/images/nmon5.png)

### 終了

Ctrl-C
