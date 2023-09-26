---
layout: post
title: Hyper-V の nat switch 使ってポートフォワーディング
date: 2021-12-18 12:38:19
tags: [Hyper-V]
---

# 何で必要になったのか

VPS でも良いけど、固定費用やスペック等考えると
自宅のマシンに建てたい、でもサーバーの脆弱性(Minecraft の log4j 問題だったり)のリスクヘッジや
管理が面倒なのでホストOS ではなくて、仮想マシンに立ててネットワークもわけたい

## 外部ネットワークスイッチじゃだめなの?

Hyper-V で 外部ネットワーク のインターフェースを作る事で、
ホストマシンと同じネットワークの ローカル IP アドレスを得られます。
このIPを持った上で、ルーターの設定画面からポートフォワーディング(ポートマッピング)設定をするだけでもサーバー公開は可能
最初はこれでも良いと思っていましたが、外部ネットワークのスイッチを作成すると次の問題が発生しました。

- 仮想マシンの上りの速度が激落ちしてた
- ホストOS も 下りの速度が激落ちしてた
- いつだって脆弱性のあるかもしれないサーバーがホストとネットワーク同じっていうのもちょっと怖い

改善策として 仮想ネットワーク アダプタ の offload を無効化する方法も色々な所に書いてあるが、解決しない

[参照](https://www.ginnokagi.com/2008/05/vmwaretcp_segmentaion_offload.html)

# 手順

## 内部ネットワークのスイッチを作る

New-VMSwitch -SwitchName vnat -SwitchType Internal

この時に出てくる InterfaceIndex が次のコマンドで必要

## 作った内部ネットワークの IPレンジを指定

New-NetIPAddress -IPAddress 172.16.2.1 -PrefixLength 24 -InterfaceIndex 57

## NAT ネットワークの作成

New-NetNat -Name vnat-nat -InternalIPInterfaceAddressPrefix 172.16.2.0/24

## ポートフォワーディング(ポートマッピング)設定

Add-NetNatStaticMapping -NatName vnat -ExternalIPAddress 0.0.0.0 -InternalIPAddress 172.16.2.22 -ExternalPort 80 -Protocol TCP -InternalPort 8080

ホストのポート80 宛の通信が来た場合、172.16.2.22 のポート 8080 に送信する

この ネットワークは dhcp サーバーはないので、Windows のネットワークアダプタ設定や、
最近の ubuntu なら netplan による固定IP設定が必要

インターネットからアクセスできる様にするには、これだけではなくてルーターから ホストマシンへのポートフォワーディングも設定しておく必要がある

