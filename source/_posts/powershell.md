---
layout: post
title: PowerShellをUbuntuにインストールする
date: 2020-02-08 00:15:47
tags: [PowerShell]
---

# 環境

- Ubuntu 18.04

# 手順

## Microsoftのリポジトリキーを追加

```bash
$ wget -q https://packages.microsoft.com/config/ubuntu/19.04/packages-microsoft-prod.deb
$ sudo dpkg -i packages-microsoft-prod.deb
$ sudo apt update
```

## dotnet-sdkインストール

dotnetコマンドでPowerShellをインストールするため、dotnet-sdkをインストールします。

```bash
$ sudo apt install dotnet-sdk-3.1 -y
```

## PowerShellインストール

```bash
$ dotnet tool install --global powershell
```

インストール完了後、ターミナルを再起動します。

## 実行できる事を確認

```bash
$ pwsh
PowerShell 6.2.4
Copyright (c) Microsoft Corporation. All rights reserved.

https://aka.ms/pscore6-docs
Type 'help' to get help.

PS /home/user>
```

## 試しにコマンドを実行してみる

PowerShellでgrepをしてみます。

```powershell
PS /home/user> echo "aaaabbbb" | Select-String "aaaa"

aaaabbbb

PS /home/user> echo "aaaabbbb" | Select-String "cccc" # 何も表示されない
```
