---
title: VagrantでMint19デスクトップ環境を立ち上げる
date: 2019-10-26 14:21:32
tags: [vagrant]
---

## virtualboxをインストール

[ここ](https://www.virtualbox.org/wiki/Downloads)からダウンロードできる

## vagrantをインストール

[ここ](https://www.vagrantup.com/downloads.html)からダウンロードできる

コマンドが使用できる様になっている事を確認する

```bash
$ vagrant --help
```

## Hyper-Vを無効化する（Windowsの場合）

PowerShellを管理者権限で起動し、以下コマンドを実行する

```PowerShell
> Disable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-All
```

## Mint19Mateデスクトップ環境を立ち上げる

### boxを追加する

ターミナルにて以下のコマンドを実行します。

```bash
$ vagrant box add antonilin/mint-19-mate
```

### プロジェクトディレクトリを作成して初期化する

```bash
$ mkdir mint19mate
$ cd mint19mate
$ vagrant init antonilin/mint-19-mate
```

### Mint19を起動

```bash
$ vagrant up
```

> **メモ**
> Windows環境では、ここでUSB2.0のサポートを無効にしろと言われたので無効にする必要がありました。
