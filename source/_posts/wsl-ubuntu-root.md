---
layout: post
title: WSLのUbuntuの初期ユーザーをrootにする
date: 2020-01-29 22:39:26
tags: [WSL,Ubuntu,BoW]
---

WSLのUbuntuを使っていて、sudoの度に「めんどくさいなあ」と思っていた時に見つけた方法です。

# 環境

- Windows 10
  - Ubuntu18.04(WSL)
  - Ubuntu16.04(WSL)

# 手順

## Windowsの機能「Windows Subsystem for Linux」を有効化する

Windowsキー -> 「機能の有効化」と検索し、「Windowsの機能の有効化または無効化」を開く -> Windows Subsystem for Linuxを探してチェックする

その後、再起動する

## Windows StoreからUbuntuをインストールする

スタートメニューから「Microsoft Store」を開く -> どれでもよいのでUbuntuをインストール

## 初期ユーザー名を「root」で指定する

スタートメニューからUbuntuを開き、ユーザー名を聞かれたら「root」と入力

既に存在しているユーザーです！(英語)と言われるが、そのまま閉じる

## 再度Ubuntuを起動する

なんと、rootでログインしています。
