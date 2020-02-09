---
layout: post
title: GitBashにgccをインストール
date: 2020-01-30 20:44:26
tags: [Git,GitBash,gcc,mingw]
---

go installしてたら「gcc.exe」が無いとビルドできないぞ！
と言われたので、mingw64のバイナリから持ってくる方法を覚えました。

# 前提

- Windows10
  - Git

# 手順

## Gitをインストール

Windows向けのGitは[ここ](https://git-scm.com/download/win)からインストーラを入手できます。

起動し、全て「はい」を選択したとして次の手順に進みます。

## MinGW-w64のバイナリをダウンロード

[ここ](https://sourceforge.net/projects/mingw-w64/files/External%20binary%20packages%20%28Win64%20hosted%29/)の下の方にあるx86_64-win32-sjljを選択しダウンロードします。

このファイルはダウンロードフォルダに置いておいてください。
解凍するために、7zipをインストールします。

## 7-zipのインストール

[ここ](https://www.7-zip.org/)からダウンロードし、インストールします。

## 解凍

GitBashを管理者権限で開き、以下コマンドを実行して解凍します。

```bash
$ cd ~/Downloads
前半は7z.exeのパス、xはeXtractのx、最後は7zipファイルのファイル名
$ /c/Program\ Files/7-Zip/7z.exe x x86_64-8.1.0-release-posix-sjlj-rt_v6-rev0.7z
7-Zip 19.00 (x64) : Copyright (c) 1999-2018 Igor Pavlov : 2019-02-21

Scanning the drive for archives:
1 file, 52785774 bytes (51 MiB)

Extracting archive: x86_64-8.1.0-release-posix-sjlj-rt_v6-rev0.7z
--
Path = x86_64-8.1.0-release-posix-sjlj-rt_v6-rev0.7z
Type = 7z
Physical Size = 52785774
Headers Size = 109370
Method = LZMA2:26 LZMA:20 BCJ2
Solid = +
Blocks = 2

Everything is Ok

Folders: 340
Files: 13669
Size:       527855563
Compressed: 52785774
```

解凍が終わると、またコマンドが打てる様になるため、mingw64フォルダが作成されている事を確認します。

```bash
$ ls
mingw64  x86_64-8.1.0-release-posix-sjlj-rt_v6-rev0.7z
```

## gccなどをGitのインストールディレクトリにコピー

GitBashを管理者権限で開き、以下のコマンドを実行します。

```bash
解凍してできたmingw64フォルダ内のbinフォルダに移動
$ cd ~/Downloads/mingw64/bin
tarで既存のファイルに上書きはしないオプションを付けて、Gitのmingw64/binにコピー
$ tar -cvf - . | tar -xvf - --keep-newer-files -C /c/Program\ Files/Git/mingw64/bin/
```

この後GitBashを起動し直すと、gccが使用出来る様になっています。
