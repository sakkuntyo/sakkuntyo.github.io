---
layout: post
title: 実家のルーターを自宅から設定したい時にした事
date: 2024-05-12
tags: [tailscale]
---

# きっかけ

[こんな方法](https://sakkuntyo.github.io/2024/02/12/udp-forwarding-tailscale-test/)で宅内のサーバーを公開していたんですが、
ふとポート開放可能な実家や別のところにラズパイでもおいて同じ事すれば VPS すら不要な事に気づきました。
ただその時に面倒になるのがブラウザ経由で行うルーター側のポートマッピング(ポートフォワーディング)設定、これを自宅内からアクセスできる様にする機能(Subnet routes)が tailscale にあったので試しました。

# 手順

OS: Raspbian 12 bookworm

1. tailscale をインストール

```
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up --accept-routes "x.x.x.x/24"
```

2. tailscale の管理コンソールからも許可

tailscale に追加マシンの 3点リーダー > Edit route settings... > Subnet routes から↑で入力した IP レンジが選択できるので、選択

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/7fc43f54-ddfa-42d9-afdc-5eeacbdc9017)

# ルーターにアクセスできるか確認

実家にいるかの様に実家のルーターのIPを指定してアクセスしてみると、表示されました。

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/cdf08663-0fa9-41c1-94ac-af138872154b)

