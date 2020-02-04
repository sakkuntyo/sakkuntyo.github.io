---
layout: post
title: nodenvでnodejsをインストール
date: 2020-02-04 23:35:33
tags: [nodejs]
---

# 環境

- LinuxMint19Mate

# 手順

## nodenvをインストール

```bash
$ git clone https://github.com/nodenv/nodenv.git ~/.nodenv
```

## nodenvのパスを通す

ターミナル起動時にパスを通す様に設定

```bash
$ echo 'PATH="${PATH}:${HOME}/.nodenv/bin"' >> ~/.bashrc
```

## initする

ターミナル起動時にinitする様に設定

```bash
echo 'eval "$(nodenv init -)"'
```

nodenvコマンドは使えるが、nodenv installコマンドはまだ使えない

```bash
$ nodenv install 12.14.1
```

## nodenvのinstallコマンドをインストール

installコマンドやuninstallコマンドを使うためにはnode-buildが必要らしい

```bash
$ git clone https://github.com/nodenv/node-build.git /usr/local/src/
$ echo 'sudo PREFIX=/usr/local /usr/local/src/install.sh' >> ~/.bashrc
```

## nodenvでnodeをインストール

ターミナルを起動し直し、以下コマンドを実行

```bash
$ nodenv install 12.14.1
$ nodenv global 12.14.1
```

## nodeとnpmのバージョンを確認する

```bash
$ node -v
v12.14.1
$ npm -v
6.13.4
```
