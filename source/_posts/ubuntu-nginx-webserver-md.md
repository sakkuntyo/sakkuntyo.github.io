---
layout: post
title: UbuntuとNginxでウェブサーバを構築する
date: 2020-01-22 23:16:15
tags: [nginx,Ubuntu]
---

# 環境

- Ubuntu16.04(KAGOYA VPS KVM)

# Nginxって何
- Apacheの代替となり得るWebサーバ

# Apacheとの違い
- C10Kをクリアしていて静的コンテンツを返すレスポンスが早い
  - C10Kとは・・・クライアント一万人接続問題の事
- イベント駆動
  - イベント駆動のおかげでスレッドを有効に使う事ができるため早い
  - 一応Apacheでもイベント駆動には出来るがNginxの方が早い

# じゃあApacheは良くないの？

Apacheの武器はそこではなく、Nginxよりも古くからユーザーに使われているため、

様々なモジュールがあり、色々な用途に使う事ができます。

> Nginxとは？Apacheとの違いについてエンジニアに聞いてみた
> https://academy.gmocloud.com/qa/20160616/2761

phpやCGIを使用した動的な処理をしたい場合にはApache
速度やアクセス数を求めたい場合にはNginx
といった使い方がよさそうです。
どっちも使って、お互いのデメリットを埋める事も出来るそうです

# 初期ページを表示するまでの手順
## ポート解放とNginxのインストール、起動
```shell-session
$ apt update

ufw(ファイアウォール)をインストール
$ apt install ufw
インストール直後はufwはファイアウォールとして指定されないためufwを有効化
$ ufw enable
「このコマンドを実行するとssh接続が切れるかも知れませんがいいですか？」と聞かれるので y を入力してEnter

sshのポートを開く
これを行わないとssh切断したあと接続出来なくなってしまいます！
$ ufw allow 22

Nginxが使用するポートを開く
$ ufw allow 80

Nginxをインストールする
$ apt install nginx

Nginxが稼働している事を確認する
$ curl localhost
curlでウェブページにアクセスすると、そのページのhtmlの内容が帰って来ます

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
![スクリーンショット 2018-07-01 23.47.42.png](https://qiita-image-store.s3.amazonaws.com/0/266455/0dc1527c-4bac-7fc5-df5a-1f8bdfebda1a.png)

Nginxではこれが初期ページとして設定されています。

# ページを追加、変更する
## ドキュメントルートを確認する
```shell-session
$ grep "root" -r /etc/nginx/ | grep "html"
/etc/nginx/sites-available/default:     root /var/www/html;
```
私の場合はこう表示されました。
Nginxのバージョンなどによってパスが違う様なので、このように調べるのが確実です。
どうやらページとなるhtmlファイルが保存されているのは　/var/www/html　ディレクトリの様です。
ここを ドキュメントルート と呼びます。
## ページを追加する
```shell-session
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
以上となります。

Apacheが気になる方はこちら
> [UbuntuとApacheでウェブサーバを立てる - Qiita](https://qiita.com/noma3629/items/03742bad0f57a4f46b07)
