---
layout: post
title: Steam ゲームのサーバーインストールとアップデート方法
date: 2024-01-27 00:00:00
tags: [Steam]
---

# 環境

ubuntu 22.04,20.04

## SteamCMD のインストール

```
sudo add-apt-repository multiverse; sudo dpkg --add-architecture i386; sudo apt update
sudo apt install steamcmd
```

## ゲームサーバーのインストール・アップデート

インストールもアップデートも以下コマンドでできる

```
steamcmd +login anonymous +app_update <appid> validate +quit
```

※ appid は [SteamDB](https://steamdb.info/app/2394010/info/) で確認、例えば 2394010 は palworld

このコマンドを実行すると、以下のディレクトリが作成される

- ~/Steam

以下のディレクトリ以下に指定したゲームのサーバーファイルが保存される

- ~/Steam/steamapps/common/

例えば palworld は以下になるが、さらにそれより下のファイルはゲームにより異なる

- ~/Steam/steamapps/common/PalServer

