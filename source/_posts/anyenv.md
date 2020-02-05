---
layout: post
title: anyenvで各env系ツールをインストールする
date: 2020-02-05 00:01:54
tags: [anyenv]
---

# 環境

- LinuxMint19 Mate

# 手順

## anyenvをインストール

### anyenvをclone

```bash
$ git clone https://github.com/riywo/anyenv ~/.anyenv
```

### パスを通す

ターミナル起動時にanyenvのパスを通す設定を書く

```bash
$ echo 'PATH=${PATH}:${HOME}/.anyenv/bin' >> ~/.bashrc
$ echo 'eval "$(anyenv init -)"' >> ~/.bashrc
$ source ~/.bashrc

anyenv用のインストールフォルダを作成する
一度だけ実行する必要がある
$ anyenv install --init
```

## インストール出来るenvを確認

```bash
$ anyenv install -l
  Renv
  crenv
  denv
  erlenv
  exenv
  goenv
  hsenv
  jenv
  luaenv
  nodenv
  phpenv
  plenv
  pyenv
  rbenv
  sbtenv
  scalaenv
  swiftenv
  tfenv
```

## 好きなenvをインストール

今回はrbenvをインストールします

```bash
$ anyenv install rbenv
インストール後、シェルを再起動させる必要がある様なので以下実行
$ exec $SHELL -l
```

## rbenvが使える事を確認

```bash
$ rbenv --version
```

## anyenvでインストールしたenvの確認

```bash
$ anyenv local -l
rbenv: no local version configured for this directory
```

## envをアンインストール

```bash
$ anyenv uninstall rbenv
rbenvが使えなくなる
$ rbenv
anyenv: env `rbenv' not installed
```
