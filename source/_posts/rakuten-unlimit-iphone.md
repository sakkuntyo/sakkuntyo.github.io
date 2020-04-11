---
layout: post
title: 楽天モバイルUN-LIMITをiPhoneで使ってみた
date: 2020-04-10 22:56:19
tags: [SIM]
---

# 楽天モバイルUN-LIMITって？

楽天が2020/4/8から開始したMNOサービス

参考：[楽天モバイルUN-LIMIT](https://network.mobile.rakuten.co.jp/)

MVNOは3大キャリアから回線の一部を借りる事で運用されていますが、
MNOは自前の回線を用いて運用します。

これまで3大キャリアのSoftBank,KDDI,docomoと言われていましたが、これからは楽天モバイルUN-LIMITが加わり4大キャリアとなるかもしれません。

# iPhoneのバージョン

- iOS 13.3.1

![0](/images/rakuten-unlimit-iphone-0.png)

# iPhoneで使えるの？ 

iPhoneでの対応は非公式となっておりますが、パートナー回線、使用量無制限の楽天回線共に接続できそうです。

iPhoneでnanoSIMを挿入して使用する場合、APNの設定は不要でそのまま使う事ができます。※
※ただし、既存のAPNプロファイルはアンインストールしてください。

eSIMを使用する場合はnanoSIMとeSIMのデュアルシム運用が可能ですが、以下の様な手順が必要となります。

# eSIMで使う手順

## マイ楽天モバイルを開く

[楽天モバイルUN-LIMIT](https://network.mobile.rakuten.co.jp/)の右上メニューにある「my楽天モバイル」から開けます。

![1](/images/rakuten-unlimit-iphone-1.png)

## nanoSIMからeSIMに契約変更

my楽天モバイルのログイン後のページから「右上メニュー」 -> 「my楽天モバイル」 -> 「契約プラン」

![2](/images/rakuten-unlimit-iphone-2.png)

「各種手続き」 -> 「SIMカード交換」　その後、SIMを変更する手続きを進めます。

![3](/images/rakuten-unlimit-iphone-3.png)

QRコードが表示されますので、このQRコードをiPhoneのカメラで読み取ります、すると、プロファイルがインストールされます。

![4](/images/rakuten-unlimit-iphone-4.png)

## パートナー回線と楽天回線の切替

しっかり確認が取れていませんが回線は自分で切り替える事ができそうです。

iPhoneにて設定アプリを開き「モバイル通信」 -> 楽天のモバイル通信プラン -> 「音声通話とデータ」を開きます。

### 楽天回線を使用する

VoLTEオフを選択します。

![5](/images/rakuten-unlimit-iphone-6.png)

### パートナー回線を使用する

VoLTEオンを選択します。

![6](/images/rakuten-unlimit-iphone-5.png)

# 速度比較

## 楽天回線接続時の速度

データが取れ次第計測します。

## パートナー回線接続時の速度

![7](/images/rakuten-unlimit-iphone-7.png)

## OCNモバイル接続時の速度

![8](/images/rakuten-unlimit-iphone-8.png)

## Nuro 2G + IEEE802.11gへのWiFi接続時の速度

![9](/images/rakuten-unlimit-iphone-9.png)

## 所感

パートナー回線のpingが比較的良好なのでスマホゲームをしてみましたが、OCNよりもちょっと不安定でした。

# これから登録する方へ

もしよろしければ紹介コードをご利用ください。

紹介コード：2020031802187
