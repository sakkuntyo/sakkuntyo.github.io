---
layout: post
title: "[hexo]hexo覚え書き"
date: 2021-07-19 23:00:07
tags: [hexo]
---

# メモ
久しぶりにhexoからブログを書いてみたら色々忘れていたのでメモ

## 動作環境
- nodejs 8.11.0
- nvm install 8.11.0;nvm use 8.11.0 した物
- nodejs 14.x.x を使用すると hexo deploy に失敗します。 

## clone
```
git clone git://github.com/sakkuntyo/sakkuntyo.github.io -b edit
```

## 記事を追加
```
$ npx hexo new 記事名
```

## 記事をコミット
```
$ git add <記事を追加で追加されたファイル>
$ git commit -m "メッセージ"
$ git push origin
```

## 記事を試しにみる
```
$ npx hexo server -D
```

-D はなんだったか忘れた

## 記事をデプロイ
```
$ npx hexo deploy -g
```
