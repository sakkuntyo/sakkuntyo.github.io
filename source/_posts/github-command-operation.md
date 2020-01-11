---
layout: post
title: GitHubをコマンド操作する
date: 2019-12-27 20:08:43
tags: [GitHub,hub]
---

GitHubにリポジトリを作りたい、
けどそのためだけにマウスを動かすのがめんどくさい、、、
そんな時に行う操作です。

# 環境

- Ubuntu18.04

# 手順

## hubコマンドのインストール

```bash
$ sudo add-apt-repository ppa:cpick/hub
$ sudo apt update
$ sudo apt install hub
```

## sshの設定

hubコマンドはsshの接続名(github.com)を使用するため、
~/.ssh/configにgithub.comの設定を記述しておく必要があります。

そのため、以下の様な内容にしておきます。

```bash
Host github.com
  Hostname github.com
  IdentityFile <githubに登録済の鍵のパス>
```

## GitHubにリポジトリを作成する

```bash
$ mkdir test-repository
$ cd test-repository
$ hub init
$ hub create
Updating origin
created repository: sakkuntyo/test-repository
```
