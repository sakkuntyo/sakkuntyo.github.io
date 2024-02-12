---
layout: post
title: 公開用のネットワークを持つために VPS を利用するとどの VPS プロバイダが快適なのか
date: 2024-02-12 20:47:50
tags: [UDP]
---

# きっかけ

今の自宅の回線がマンション共用の物なので、ルーターがいじれません。
ルーターがいじれないという事はインターネットからのアクセスのポートマッピング(ポート開放)ができませんでした。
ただ、回線の速度や安定感はあるので追加で回線を契約するほどのコストをかけたくないですし、
今までは宅内サーバーをインターネットに公開するために ngrok (HTTPやTCP) や localtonet (UDP) を利用して公開していましたが、
localtonet は 日本サーバーが無いために、ping 値が高くなる等、歯がゆい状況でした。

そこで他に方法ないかなと探していたら見つけました。
tailscale の exitnode を利用し、インターネットからのアクセスを受けた VPS から tailscale ネットワーク内のマシンにポートフォワーディングして、
VPS のマシンが実質ルーター代わりになるという方法

[例えば yayoi_8128 さんのこんな方法](https://note.com/yayoi_8128/n/n4a35f271a57f)

ポートフォワーディングについては、uredir を使わずに nginx や iptables でフォワーディングの設定をする、でもよかったんですが、以下の理由で uredir を採用してます。

- uredir のコマンドが覚えやすかった (uredir :8211 フォワーディング先IP:8211)
- iptables のコマンドを覚えるのがむずかしかった
- 実際に nginx を使用して比較しても体感できる差が感じられなかった

Azure, Sakura, WebArena の VPS それぞれで パルワールドサーバーのUDP フォワーディング を試した結果、安定性や速度が異なったので感想とともに記録を残します。

# テスト環境の構築

OS: ubuntu 22.04 server

1. tailscale をインストールして exitnode を有効化

```
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up --advertise-exit-node
```

2. tailscale AdminConsole から "Use as exit node" にチェック

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/aa7549a0-b4ad-4476-836f-2a50b91a66d9)

3. IPv4 フォワーディングを許可
```
echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
sudo sysctl -p /etc/sysctl.d/99-tailscale.conf
```

4. その他

vps 側で 22 や 8211 の inbound を許可

# 注意点

その時たまたま VPS プロバイダ側で障害があったとか、一時的な問題が起きていた可能性もあるのであくまで参考程度にしてください。

条件もきっちり揃えられていません。

## Azure VM

### テストに利用したスペック

- コア数とメモリ: 1コア1GB
- ネットワーク: 100Mbps
- 金額: 1271円/月 以上

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/2a7385e9-edc7-4aff-b9c2-db9b938c47c2)

### 速度

速度は出ているけど、レイテンシの値が高い。
何故かコロンビアやインドのサーバーを利用してました。

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/619e76a1-7488-42d1-8b78-a71425505937)

念のため別のサイトでも試してみる。

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/0ea0ce1c-67e2-458e-a3b9-5f41b4d2eda1)

Ping も Jitter も良好

### パルワールドを遊んでみる

ロードがなかなか終わらない・・・

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/58523e70-1ece-4ef8-beb3-899f968a04d5)

10分程度待てば接続はされた。
とはいえ建築物の表示にもかなりの時間がかかるため遊ぶのはきびしそう

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/5348a238-ee87-480c-a586-4da87d6d727c)

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/1347118a-8921-4d15-83af-373024355511)

### その他気になった事

tailscale up したときに見覚えのないログが出た、何か改善の余地あり？

> Warning: UDP GRO forwarding is suboptimally configured on eth0, UDP forwarding throughput capability will increase with a configuration change.

[この方法](https://tailscale.com/kb/1320/performance-best-practices#ethtool-configuration)で最適化されるらしいですが、残念ながら体感できず。。。

- 翻訳
> Linux 6.2 以降のカーネルで Tailscale バージョン 1.54 以降を使用すると、[トランスポート層のオフロード](https://www.kernel.org/doc/html/latest/networking/segmentation-offloads.html)によって UDP スループットが向上します。

```
NETDEV=$(ip route show 0/0 | cut -f5 -d' ')
sudo ethtool -K $NETDEV rx-udp-gro-forwarding on rx-gro-list off
```

## Sakura VPS

### テストに利用したスペック

- コア数とメモリ: 2コア1GB
- ネットワーク: 100Mbps
- 金額: 990円/月

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/3584674e-7686-41ce-ac1a-6c6242b0c144)

### 速度

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/e2d4d5fb-c414-4210-9177-8fee6df39364)

### パルワールドを遊んでみる

tailscale ネットワークだけで接続するのと体感は変わらず快適

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/f2b8f741-d22e-48bc-8119-34f9125d4aa3)

## WebArena Indigo 

### テストに利用したスペック

- コア数とメモリ: 1コア1GB
- ネットワーク: 100Mbps
- 金額: 449円/月

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/dc36abca-ef66-4750-942f-0f748d32afce)

安くてよさそう

### 速度

ちょっと遅いかな

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/e913b1f1-c2f4-44bc-9243-83c3b22c00e8)

### パルワールドを遊んでみる

なんだかパケロスが激しい

接続してから数十秒の間、建築物のオブジェクトが読み込まれず、これで遊ぶのは厳しそう、と感じました。

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/9d4fa4b1-1d90-43d3-8403-d4a979ba8786)

## Conoha VPS

### テストに利用したスペック

- コア数とメモリ: 2コア1GB
- ネットワーク: 100Mbps(インターネット)
- 金額: 1064円/月(時間課金)

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/69874dd2-944f-4109-bdcf-7d895b65be13)


### 速度

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/2f037fd9-d50d-4a0c-a5ec-47c6dd220f1c)

### パルワールドを遊んでみる

ロード時間がそこそこ長くかかった

建築物等がなかなか読み込まれず、表示されるまでに5分くらいかかった

Azure VM を少しマシにした様なレベルで、これで遊ぶのは厳しい

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/f4089f75-87a6-4d2d-a171-823d40264232)

## その他

### 採用されたのは・・・

さくら VPS でした。安定感がどエライです。
Azure VM の回線速度が優秀なので、これをどうにかモノにできないか気になります。

### 他の VPS について

他に試したい VPS もいくつかあるので試したら追記していきます。
