---
layout: post
title: 「npm install -g」はもう要らない！npxの使い方
date: 2020-02-01 00:11:50
tags: [npm,npx]
---

今まで、hexoやexpress-generatorのコマンドラインツールを使用するためには、
npm install -g をしてプロジェクト外にインストールする必要がありました。
npm5.2.0ではnpxが追加され、プロジェクト内にインストールした場合でも使用出来る様になりました。

これからは、プロジェクト内にhexoやexpress-generator等をインストールしておけば使えます。

# 環境

- Ubuntu18.04

# npxを使わない場合

```bash
expressが見つからないと言われる
$ express express-project

グローバルインストールする
$ npm install -g express-generator

コマンドが使える様になる
$ express express-project
```

# npxを使う場合

```bash
expressが見つからないと言われる
$ express express-project

プロジェクトにインストールする
$ npm install express-generator

npxでプロジェクト内のexpressを実行
$ npx express express-generator
```
