---
layout: post
title: WSLのUbuntuでbyobuを使う
date: 2020-02-13 23:14:06
tags: [wsl,byobu]
---

# 環境

- Windows10
  - Ubuntu 18.04
    - byobu 5.125

# 手順

## [byobuをインストール](https://sakkuntyo.github.io/2020/02/05/byobu/)

## bash起動設定

.bashrcに以下一行を追記する
曖昧文字幅を全て全角幅にする設定です。

```bash
export VTE_CJK_WIDTH=1
```

