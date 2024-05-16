---
layout: post
title: Raspberry Pi の温度
date: 2024-05-17
tags: [Raspberry Pi]
---

# 背景

ラズパイ5、動作は非常にいいんですが実際に温度を見たらファンレス運用はちょっと厳しそうな気がしたのでファンを購入しました。

過去のラズパイでは熱なんか気にならなかったんですけどね。。。

普段から PC の温度は見る様にしてますが、個人的には厳しめには見てないですが、異常な状態は回避したいなと

## 温度を見るときの基準

1. スロットリングが発生する温度に到達していないかどうか
2. 他のユーザーと比べてアイドルの温度が高くないか

1 はマストです。
2 以降は情報が見つからない場合もあるので優先度低

例えば Ryzen 3950X はアイドル時の周波数と温度が高くなりすぎるため、コアブーストを切って 3400 Mhz で運用したりとかしてます。

(Ryzen 5950X ではこの問題が解決されている様なので、5950X がうらやましい) 


# 各ラズパイで観測した温度

OS : Raspberry Pi OS (bookworm)

複数回コマンド実行して、外れ値ではなさそうだな、という事だけ見てます。。

## Raspberry Pi Zero W/H (ヒートシンクのみ)

ケースについてきたヒートシンクをつけています

### Homebridge 起動中

```
$ vcgencmd measure_temp
temp=45.5'C
```

## Raspberry Pi 2

何もつけてません。

### 特になにもさせてない時

```
$ vcgencmd measure_temp
temp=45.5'C
```

### tailscale の exit node にして速度測定中

```
$ vcgencmd measure_temp
temp=53.0'C
```

## Raspberry Pi 3 (ヒートシンクつき)

ヒートシンクはプラスチックケースについてきた黒いやつ


### 何もさせてない時

```
$ vcgencmd measure_temp
temp=53.7'C
```

### tailscale の exit node にして速度測定中

```
$ vcgencmd measure_temp
temp=64.5'C
```

## Raspberry Pi 4 (ケースファンつき)

たまたま買った[このケース](https://www.amazon.co.jp/gp/product/B07VB24K9W?ie=UTF8&psc=1&linkCode=ll1&tag=noma362907-22&linkId=ab42156e7f1536101bcae681defe5910&language=ja_JP&ref_=as_li_ss_tl)についてきたファンで、アクティブクーラーではないです。かなり静かで作業用のデスクにおいといても気にならない
アクティブクーラーだと OS や ファームからコントロールできない特殊な環境では爆音になるので、
コントロールのしようがないこういうファンの方がいいかも。

### 何もさせてない時

```
$ vcgencmd measure_temp
temp=38.9'C
```

### tailscale の exit node にして速度測定中

```
$ vcgencmd measure_temp
temp=48.7'C
```

## Raspberry Pi 5 (ヒートシンクのみ)

[このケース](https://www.amazon.co.jp/gp/product/B0CXPH1PZH?ie=UTF8&psc=1&linkCode=ll1&tag=noma362907-22&linkId=5200b4c6e5b1fb01e380fb5931adafc2&language=ja_JP&ref_=as_li_ss_tl)とこれについてきたヒートシンク(銅)を使用

ただ Raspberry Pi OS を起動するだけでアッツいので今までのとは違う事がわかります。
ギリギリ手で持てるかな、くらいの熱さ


### 何もしてない時

ファン装着後の測定が面倒でしていません。75'Cくらいだったかと。

### Minecraft Server 起動中

ファン装着後の測定が面倒でしていません。83-90'Cくらいでした。

90'C 到達時はサーマルスロットリングが発生してるのでは？と思い、パフォーマンスに不満はありませんでしたがファン購入に至りました。

## Raspberry Pi 5 (ファンつき)

[このアクティブ クーラー](https://www.amazon.co.jp/gp/product/B0CX4DFY8G?ie=UTF8&psc=1&linkCode=ll1&tag=noma362907-22&linkId=a37e14832a55eebb1836ec43d637feca&language=ja_JP&ref_=as_li_ss_tl) を追加しました。

アクティブクーラーだとファンの回転速度が温度によって自動変速します。

ケースと同時についてきた NVMe HAT とも同時に使えていて満足

ただ、ドライバ対応が微妙な Windows を起動した時は最高速度で回転しつづけていて、非常にうるさい。

自作PC経験上の推測・・・ファン自体が小さい事、最大回転数が高い事、このファンと一体化してるヒートシンクの距離がファンと近い事全てがうるさくなる原因だと思う。

ただし、NVMe ハットがケース内のスペースをとっているので、他の選択肢が見当たるわけでもない

### 何もしてない時

ファンの回転数は 75 

```
$ cat /sys/devices/platform/cooling_fan/hwmon/hwmon3/pwm1
75
```

```
$ vcgencmd measure_temp
temp=56.0'C
```

### Miecraft Server 起動中

ファンの回転数は 125

```
$ cat /sys/devices/platform/cooling_fan/hwmon/hwmon3/pwm1
125
```

```
$ vcgencmd measure_temp
temp=63.1'C
```

# 気づき

ラズパイ5のアクティブクーラーの回転速度は 50ずつ増加・減少される様です。75, 125, 175 等

これは pwm1 の内容であって実際の回転速度ではない事に注意
pwm1 は 255 まで指定できる様で、これが購入したファンの回転数 8000 だと思います。


# アクティブクーラーの騒音対策

アクティブクーラーの騒音について、温度が高くなるとかなりの速度でファンが回転し、結果うるさくなります。

↓の様なパワー系の対処をして回避しています。

/etc/crontab に以下を記載して、1秒に1回ファンの回転数を指定し、静かな速度(110以下)で動作させています。

1秒毎なので自身の環境では 一瞬 125や175になるタイミングがありました。

```
@reboot root while true;do sleep 1;echo 75 | tee /sys/devices/platform/cooling_fan/hwmon/hwmon3/pwm1;done
```

[しっかりやろうとする](https://forums.raspberrypi.com/viewtopic.php?t=362528)と、冷却マップの再構築と設定外出しために再コンパイルが必要になる様子、ここまではやらなくていいかな。

