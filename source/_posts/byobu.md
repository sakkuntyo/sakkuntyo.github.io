---
layout: post
title: ターミナルでタブみたいな機能が使える、byobuの使い方
date: 2020-02-05 23:54:39
tags: [byobu]
---

[byobu](https://byobu.org/)を使うと、一つのターミナルで複数のプロンプトが使えます。

実行と同時にリソースの消費具合を確認したいから、右側にnmon、左側でvim、なんて事が出来る様になります。

内部ではtmux(ターミナルマルチプレクサー)が動いていて、
byobuはtmuxをショートカットベースで使いやすくしてくれます。

![byobu](/images/byobu1.png)

# 環境

- Ubuntu 18.04

# インストール

```bash
$ apt update
$ apt install byobu -y
```

# 使い方

## byobuを起動する

```bash
$ byobu
```

以降の全てのショートカットはbyobuを起動した状態で行います。

## 画面を垂直に分割する

トップの画像はターミナルを垂直に分割した物です。

Ctrl-F2

![垂直に分割](/images/byobu-vertical.png)

## 画面を水平に分割する

Shift-F2

![水平に分割](/images/byobu-horizon.png)

## 分割された他のプロンプトにフォーカスを移動

操作するプロンプトを変更したい時に

- 次へ
  - Ctrl-F4
- 前へ
  - Ctrl-F3

![フォーカス移動前](/images/byobu-focus1.png)
![フォーカス移動後](/images/byobu-focus2.png)

## 分割されたプロンプトの移動

- 次へ
  - Shift-F4
- 前へ
  - Shift-F3

![移動前](/images/byobu-move1.png)
![移動後](/images/byobu-move2.png)

## 新しいウィンドウを作成

F2

![新規ウィンドウ](/images/byobu-newindow.png)

## 他のウィンドウに移動

- 次へ
  - F4
- 前へ
  - F3

![ウィンドウのフォーカス移動](/images/byobu-focus-window.png)
![ウィンドウのフォーカス移動](/images/byobu-focus-window.png)

## 分割されたプロンプト(ウィンドウ)を終了

終了したいプロンプトにフォーカスし、exitします。

```bash
$ exit
```

![終了](/images/byobu-exit1.png)
![終了後](/images/byobu-exit2.png)

## 画面の共有

他の人と同じ所にSSHした状態でbyobuを起動すると、同じ画面(セッション)を共有できます。

気になる方は試してみてください。
