---
layout: post
title: nodejsをインストール【Windows・Mac・Linux】
date: 2019-11-16 00:33:17
tags: [windows,mac,mac,nodejs,map]
---

## 3OSで同じ手順でできます

WindowsはWSLを入れ、WSLからコマンド操作を行います。

## 手順

### nvmをインストール

```bash
$ git clone https://github.com/creationix/nvm ~/.nvm
```

### パスを通す

```bash
$ source ~/.nvm/nvm.sh
```

### 次回ターミナル起動時に自動でパスを通す

```bash
$ echo "source ~/.nvm/nvm.sh" >> ~/.bashrc
```

### nodejsとnpmをインストール

```bash
$ nvm install --lts
# バージョンを指定するのであれば --lts の代わりにバージョンを入力
```

### nodejsのバージョンを確認

```bash
$ node -v
```

### npmのバージョンを確認

```bash
$ npm -v
```
