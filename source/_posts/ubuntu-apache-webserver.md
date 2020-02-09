---
layout: post
title: UbuntuとApacheでウェブサーバを構築
date: 2020-01-23 00:54:51
tags: [Apache,Ubuntu]
---

# 環境

- Ubuntu 16.04(KAGOYA VPS KVM)

# Apacheって何
- ブログやホームページを公開するために使う事が出来るウェブサーバ

# 特徴
- phpやCGIを用いた動的コンテンツの表示が出来る
- リバースプロキシとしても使用できる
- 使われ始めてからの歴史が長い

# 初期ページを表示するまでの手順
## ポート解放とApacheのインストール、起動
```
$ apt update

ufw(ファイアウォール)をインストール
$ apt install ufw

インストール直後はufwはファイアウォールとして指定されないためufwを有効化
$ ufw enable

「このコマンドを実行するとssh接続が切れるかも知れませんがいいですか？」と聞かれるので y を入力してEnter

sshのポートを開く
これを行わないとssh切断したあと接続出来なくなってしまいます！
$ ufw allow 22

Apacheが使用するポートを開く
$ ufw allow 80

Apacheをインストールする
$ apt install apache2

Apacheが稼働している事を確認する
$ curl localhost && echo success || echo failed

successと表示されればApacheは起動出来ています。
表示された長いhtmlはデフォルトページのhtmlソースです。

自分のIPアドレスを確認する
$ ifconfig | grep "inet addr:"

192.168.1.xや127.0.0.1といったIPアドレスが表示されると思います
これらはローカルIPや、グローバルIPと呼ばれます。
127.0.0.1は、ループバックアドレスと呼ばれ、自分自身を表すIPアドレスとなります。
```

## 実際にページを表示してみる
同じネットワーク内の他のPCからウェブサーバを利用してみます。
ブラウザを起動し、先ほど確認したローカルIP、又はグローバルIPをアドレスバーに入力します。

このような画面が表示されると思います。
![スクリーンショット 2018-07-02 2.04.52.png](https://qiita-image-store.s3.amazonaws.com/0/266455/3ffbc0f8-a777-8a56-1fdb-6d4a7d984857.png)
Apacheではこれが初期ページとして設定されています。

# ページを追加、変更する
## ページを追加する
Apacheがブラウザに送ってくれているhtmlは /var/www/html/ となっている様です。
ここを ドキュメントルート と呼びます。
ここにファイルを配置する事でApache経由で参照する事ができるようになります。
```
ドキュメントルートに移動する
$ cd /var/www/html/
新しいページのファイルを作成する、アクセスする際のページ名は「test.html」とします
$ echo "Hello World!" > ./test.html
```

## 実際にページを表示してみる
他のPCからページを
同じネットワーク内の他のPCからウェブサーバを利用してみます。
ブラウザを起動し、下記のようにアドレスバーに入力します。
```IPアドレス/test.html
```

この様な画面が表示されます。
![スクリーンショット 2018-07-02 0.07.53.png](https://qiita-image-store.s3.amazonaws.com/0/266455/a7714f81-4a06-a4f4-4d12-09b361f9d3d1.png)
以上となります、Nginxが気になる方はこちら
> https://qiita.com/noma3629/items/807f25f9eb13525eebef

