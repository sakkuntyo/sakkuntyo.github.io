---
layout: post
title: Go製CMS ponzuを試してみた
date: 2020-02-02 03:36:06
tags: [golang,cmd,ponzu]
---

CMSを作りたくて、[この動画](https://www.youtube.com/watch?v=T_1ncPoLgrg)を見ながら試してみました。

# ponzuとは

Goで作られているヘッドレスCMS

[ponzu - GitHub](https://github.com/ponzu-cms/ponzu)

# 環境

- Go 1.13.5

# 使い方

## インストール

```bash
$ go get -u https://github.com/ponzu-cms/ponzu/...
```

## ponzuプロジェクト作成

以下コマンドでGOPATH/src以下にプロジェクトが作成される

```bash
$ ponzu new github.com/sakkuntyo/ponzu-project
```

以下cd先にプロジェクトが作られている

```bash
$ cd ${GOPATH}/src/github.com/sakkuntyo/ponzu-project
$ ls
CONTRIBUTING.md  Dockerfile  LICENSE  README.md  addons  cmd  content  deployment  docs  examples  ponzu-banner.png
```

この後の操作はこのデイレクトリ内で行う

## テンプレコードを作成

```bash
テンプレートコード作成
ponzu generate content コンテンツ名 コンテンツ内のデータ名:データ型:[入力方法] [コンテンツ内のデータ名:データ型:[入力方法]] ..
$ ponzu generate content author name:string photo:string:file bio:string:richtext
これでテンプレートコード(content/author.go)が作成される
```

## ponzuをビルド

```bash
$ ponzu build
これでponzu-server、及び実行に必要なライブラリ(cmd以下)が配置される
```

## ponzu起動

```bash
$ ponzu run
何故かうまくいかないが、もう一度実行すると起動できる
$ ponzu run
Server listening at localhost:8080 for HTTP requests...

Visit '/admin' to get started.
```

起動中にlocalhost:8080/adminにアクセスする事でCMSのGUIが表示される

# CMSで出来ること

## 記事の追加

左メニューからコンテンツを選び、NEWを選択する事で、記事が書ける

SAVEをすると、内容がsystem.db(BoltDB)に保存される

## 書いた記事の参照

json形式で記事が参照できる、確認してみる

```bash
Authorをgenerate、記事追加したとして、以下コマンドで確認
$ curl "localhost:8080/api/content?type=Author&id=1"
{
    "data": [
        {
            "bio": "ponzu\u305f\u3081\u3057\u3066\u307f\u305fbio",
            "id": 1,
            "name": "ponzu\u305f\u3081\u3057\u3066\u307f\u305f",
            "photo": "/api/uploads/2020/02/4fd4c0e572a4fed83f1d1dc5e64a2ab8600.jpg",
            "slug": "author-77f9980f-db1e-421b-bd3b-ce0879e9d670",
            "timestamp": 1580577064000,
            "updated": 1580577184147,
            "uuid": "77f9980f-db1e-421b-bd3b-ce0879e9d670"
        }
    ]
}
```

これをブラウザ側でプレビューしてあげたりするとブログっぽくなるのかな

