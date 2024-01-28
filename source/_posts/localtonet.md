---
layout: post
title: localtonet で UDP ポートフォワーディング
date: 2024-01-28 20:26:38
tags:
---

# 必要になった経緯

ゲームサーバーを自宅で立てるとなると、外からでもそのサーバーにアクセスできる様にポート開放する必要がありますが、
引っ越しをしてからマンション共有の回線を使っているためにルーターの設定ができず、ポート開放できない環境なため別の方法を探しました。
ただ、回線の品質は特に悪くないので自分で回線を契約するのはちょっともったいない・・・と思い別の方法をとりました。
localtonet への課金もしてみましたが、複数のフォワーディングをしない限り無料枠で事足りそうな雰囲気

# localtonet の使い方

## localtonet に登録

とりあえず登録します。

## token をコピー

ダッシュボードに表示される AuthToken をコピーしておく

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/890efed4-6373-4cf3-bc9c-8c9dd80d06c3)

## tunnel を作成し起動しておく

My Tunnels > TCP - UDP から作成する

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/56a08ba0-40de-42f4-9036-97053b4273af)

Protocol Type と Server, ローカルのポートを指定して Create
作成されたら Start もクリックしておく
![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/04745fa5-9e28-4726-bd35-824d2d5805e7)

## サーバー側でやる事

localtonet をインストールして次のコマンドを実行

```
localtonet authtoken <token>
```

すると以下の様に tunnel が表示されれば OK
![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/b5ed9d2d-dd2e-4a91-a941-d50f24209cb0)

IP/Url に表示されたアドレスに接続できる様になっているはず。

# ngrok じゃだめ？

ポートフォワーディングしてくれる有名なツールに ngrok がありますが、そちらは UDP のフォワーディングはできません。

# その他所感

## リージョンに日本がない・・・
どこのサーバーを経由するか選べますが、日本がありません。ngrok では勝手に日本サーバー使ってくれるけど・・・
中国を選んで使っていて以外とラグも感じないですが、日本サーバーが使えたらよかったな

## 外部から見たポートの固定は有料でも無料でもできない
localtonet を起動する度に外部から見たポート番号が変わります。
なのでサーバーを複数人で利用している場合、 localtonet を再起動したあとは新しいポート番号の接続先を共有する必要が出てきます。
これは ngrok の有料プランだとできたとおもうので、ちょっとおしい
