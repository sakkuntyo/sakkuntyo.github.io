---
layout: post
title: WSLからWindowsのドライブをマウントする
date: 2020-02-12 02:20:50
tags: [wsl]
---

# 環境

- Windows10
- Ubuntu 18.04

# 手順

## マウント

マウントしたいドライブのドライブレターを確認し、以下コマンドを実行

今回はドライブレターはAとします。

```bash
$ mkdir -p /mnt/a
$ mount -t drvfs A: /mnt/a
```

## アンマウント

```bash
$ umount /mnt/a
```
