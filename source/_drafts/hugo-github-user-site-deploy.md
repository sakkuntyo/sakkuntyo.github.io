---
layout: post
title: Hugo + GitHub Pagesでブログを構築する【ユーザーサイト】
date: 2020-01-23 21:29:04
tags: [Hugo,GitHub]
---

# 環境

- Ubuntu 18.04(WSL)

# Hugoとは

静的サイトジェネレータ

マークダウンで書いた記事を
用意したテンプレートファイルに合わせてhtmlファイルにしてくれる

※このブログはHexoを使用して作成されています。

# GitHub Pagesとは

GitHubに決まった形でリポジトリを置いておく事で、
ファイルをホスティングしてくれるサービス
ユーザーサイト、プロジェクトサイトの二種類がある

- ユーザーサイト
  - <username>.github.ioのmasterブランチをホスティングする
  - URLは https://<ユーザー名>.github.io でアクセスできる
- プロジェクトサイト
  - プロジェクト名は何でも良く、gh-pagesブランチをホスティングする
  - URLは https://<ユーザー名>.github.io/<プロジェクト名> でアクセスできる

# 何故GitHub Pagesなのか

- メリット
  - WordPressの様に実行環境が要らない
  - デフォルトでhttpsが使える
  - 上記理由でVPSを借りたり、ドメインや証明書を取る必要がないためお金がかからない
  - GitHubで記事を管理するので管理が楽、どこからでも出来る
  - 定期アップデートが必要ない
  - 引っ越ししやすい
    - HugoからJekyllやHexoに移行する場合に移動させるマークダウンはほとんど同じルールで記述されるため

# 前提

- GitHubにSSH鍵が登録されている事
  - やり方がわからない方は[こちら](https://sakkuntyo.github.io/2019/10/20/github-addkey/)の記事を参考にしてください
- Hubコマンドがインストールされている事
  - やり方がわからない方は[こちら](https://sakkuntyo.github.io/2019/12/27/github-command-operation/)の記事を参考にしてください

# 手順

## Hugoのダウンロード、インストール

[GitHubリリースページ](https://github.com/gohugoio/hugo/releases)から環境にあった物をダウンロードし、インストールします。

Ubuntuの場合は以下コマンドでHugo0.62.2(現在最新)をダウンロードできます。

```bash
$ wget https://github.com/gohugoio/hugo/releases/download/v0.62.2/hugo_0.62.2_Linux-64bit.deb
$ sudo dpkg -i hugo_0.62.2_Linux-64bit.deb
```

以下コマンドでHugoが使える事を確認しておきます。

```bash
$ hugo version
```

> **ポイント**
> Windowsの場合はインストール形式になっていないため、環境変数のPATHにhugo.exeがあるフォルダを追加してあげる事で使用出来る様になります。

## GitHubにリポジトリを作成する

ユーザーサイトのホスティングをする場合は、
GitHubに以下の名前でリポジトリを作成します。

```
<ユーザー名>.github.io
```

私の場合はsakkuntyo.github.ioというリポジトリを作成します。

今回はhubコマンドでリポジトリを作成します。

```bash
$ mkdir <ユーザー名>.github.io
$ cd <ユーザー名>.github.io
$ hub init
$ hub create
```

## 編集用ブランチに切り替える

masterにはホスティングするページのみを配置したいため、editブランチを作成し、editブランチで作業を行います。
作業ブランチは別のリポジトリでも問題ありません。

```bash
$ git checkout -b edit
```

## プロジェクト作成

HelloBlogという名前でブログを作成します、これは後から変更する事が可能です。

```bash
HelloBlogという名前でプロジェクトフォルダが作成されます
$ hugo new site HelloBlog
中身をリポジトリルートに移動します
$ mv HelloBlog ./
フォルダは必要ないので全て削除します
$ rm -r HelloBlog
プロジェクトの中身を確認します
$ ls
archetypes  config.toml  content  data  layouts  static  themes
```

## テンプレート追加

Hugoの作成するプロジェクトには初期テンプレートが入っていないため、
テンプレートを自分で追加する必要があります。
大抵のテンプレートはthemesフォルダにgit cloneしてあげる事でそのまま使用できます。

今回は、[easybook](https://github.com/Y4er/hugo-theme-easybook.git)を使用したいと思います。

```bash
themesフォルダにeasybookという名前で保存される様、cloneします
$ git clone https://github.com/Y4er/hugo-theme-easybook.git theme/easybook
```


