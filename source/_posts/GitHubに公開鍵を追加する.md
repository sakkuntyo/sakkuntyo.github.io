---
title: GitHubに公開鍵を追加する
date: 2019-10-20 12:42:45
tags: [GitHub]
---

# 前提環境

- Ubuntu

# GitHubに公開鍵を追加する理由

- sshを使ってリモートリポジトリの操作を出来る様になる
- GitHub上にあるリポジトリをsshで操作する様に作られた手順、ツールが沢山ある

> **注意**
> sshを使わなくてもhttpで操作する事が可能
> ただし、その場合はGitHubアカウントのパスワード入力が多々必要になる

# 手順

## 秘密鍵・公開鍵を作成する

```bash
$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): sakkuntyo-mint #鍵の名前です、今回はLinuxMint用に作成したためこの名前
Enter passphrase (empty for no passphrase): #パスワード、無くても良い
Enter same passphrase again: #パスワードの再確認
Your identification has been saved in sakkuntyo-mint.
Your public key has been saved in sakkuntyo-mint.pub.
The key fingerprint is:
SHA256:7XG5j/GRtAxIs3/dkUxVIZDrcyG+6g7LVxqvNVK1bEg root@DESKTOP-2QSQU2N
The key's randomart image is:
+---[RSA 2048]----+
|           .o. .=|
|           .  . .|
|          oE.. . |
|         o.*+o+ .|
|        S Bo=+o+ |
|         o.O.* +o|
|       . .*oB * o|
|      . oooo.* . |
|       o+=o . o  |
+----[SHA256]-----+
```

## 鍵ファイルが出来た事を確認する

```bash
$ ls
sakkuntyo-mint sakkuntyo-mint.pub
```

.pubが付いているのが公開鍵
ついていないのが秘密鍵

## GitHubに配置する

### github.comのsettingsを開く

![github-settings](/images/github-settings.png)
![github-settings2](/images/github-settings2.png)

### 「SHS and GPG keys」を開き、公開鍵の名前と公開鍵の内容を登録

Titleは何でも大丈夫

![github-settings](/images/github-settings-keys.png)
![github-settings](/images/github-settings-keys2.png)

これで公開鍵が登録されました

## sshクライアントにgitの設定を追加

~/.ssh/configを編集し、以下の4行を追加

```
Host git
  hostname github.com
  user git
  identityfile ~/.ssh/sakkuntyo-mint #秘密鍵のパス
```

秘密鍵をconfigで指定した場所に置きなおす

```bash
$ mv sakkuntyo-mint ~/.ssh/
```
秘密鍵の権限を自分だけが読める様に変更

```bash
$ chmod 0600 ~/.ssh/sakkuntyo-mint
```

## プライベートリポジトリをcloneしてみる

プライベートリポジトリをhttpでcloneしようとするとパスワードが求められますが
sshを使ってcloneした場合にはパスワードは求められなくなります

```bash
$ git clone git:sakkuntyo/private-repo
```
