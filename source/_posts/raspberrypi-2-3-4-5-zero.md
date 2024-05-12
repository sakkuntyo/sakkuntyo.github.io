---
layout: post
title: Raspberry Pi の用途
date: 2024-05-12
tags: [Raspberry Pi]
---

最近何かとサーバーを立てる事が多く、今まで購入するだけして眠ってたラズパイ達が活躍し始めてるので用途を紹介


# 用途

## メモリが 1GB 以下の Raspberry Pi

zero 1.1 や 2 や 3 が該当

- tailscale exit node や subnet routes 用 [こんな用途](https://sakkuntyo.github.io/2024/05/12/tailscale-advertise-routes/)
- [Home Bridge 用](https://qiita.com/zizi4n5/items/1683d3c3a62eee2cdbb2)
デスクトップ版 OS を使うとそれだけでメモリがカツカツになるので、可能であればサーバー版 OS を使う事をおすすめ

1GB モデルの場合
デスクトップ版の空きメモリ 200MB 程度
サーバー版の空きメモリ 700MB 程度

[raspberry pi zero 購入リンク - amazon](https://www.amazon.co.jp/Raspberry-Pi-Zero-WH-%25E3%2583%2598%25E3%2583%2583%25E3%2583%2580%25E3%2583%25BC%25E4%25BB%2598%25E3%2581%258D/dp/B07BHMRTTY/ref=sr_1_5?__mk_ja_JP=%25E3%2582%25AB%25E3%2582%25BF%25E3%2582%25AB%25E3%2583%258A&amp;crid=1J2TUV5FFV8MZ&amp;dib=eyJ2IjoiMSJ9.AjTkYGEWZj-JsV1QsqVMa1rWz7oawWrUTKwEMFa7HFqhvDygDJQ5qhz12F886Mt9OgwE2H9FQz2gaiBc9jE2oeXCvzAIZfBPTBBWaVliorfZ5L3JwfkTJlrUP5x4vUHP55yc_2vRAFmpow6s-GrGB3dCJvnlmvuOKlmWazHfb86hP4enwPvUoRVXDuCWiC100yHYGJzh3QC9lj9gm_04-cGf6MlhJWsx5GD-5pwPw6nRXDTFaCUN8CX96RocHpypmdW6W-k06wdusyN7OWAXddyMq1UAgUj60vgMyIGWdZg.2mcp9DB1OgHI0qC2T5aHNg8-TOTV9id_N7bWpQ5YOU4&amp;dib_tag=se&amp;keywords=raspberry+pi+zero&amp;qid=1715473067&amp;sprefix=raspberry+pi+zer%252Caps%252C175&amp;sr=8-5&_encoding=UTF8&tag=noma362907-22&linkCode=ur2&linkId=959bc239a7042ec66a439aa08b91a8cd&camp=247&creative=1211)

[raspberry pi zero 2 購入リンク - amazon](https://www.amazon.co.jp/%25E3%2580%25902021%25E5%25B9%25B4%25E6%2596%25B0%25E5%2587%25BA%25E3%2580%2591Raspberry-%25E3%2583%25A9%25E3%2582%25BA%25E3%2583%2599%25E3%2583%25AA%25E3%2583%25BC%25E3%2583%2591%25E3%2582%25A4-W%25EF%25BC%25882%25E4%25BB%25A3%25EF%25BC%2589RAM%25E5%25AE%25B9%25E9%2587%258F-CPU%25E9%2580%259F%25E5%25BA%25A61GHz-Cortex-A53/dp/B09N8LMWLS/ref=sr_1_2?crid=3BT01N12FN5KS&amp;dib=eyJ2IjoiMSJ9.OwbalKiYU86-rquZUxojf1b3YjOcvHrZScb6VP6lVvurbQ9zPUxYJZoa10l0rt72c6KmhfHg1ftp5l8m9NNviavqAa1Bs6ZKIrYblhi0MCxgoIPch9eI3MQLLZwQcp6So9nnfTY4kM6yBT1xf4yqMrJaOESpUK8FQUcZFOhPDYVOKCrka3HsaeracIJzlrOhBP63xz15wUWHUpUOCJn0mbveNR4tFBBpBuq7javIohvoX_61jVM6LLLLlmRv7DTtf6REPpYBsihUc79ZR_OeWVrsfwffLC_sYu2Zo11efdU.CDcOs0z31uKQ3wZ7O-8c5kqVUjZysniLHYdHbTPiqrg&amp;dib_tag=se&amp;keywords=raspberry+pi+zero+2+w&amp;qid=1715473314&amp;sprefix=raspberry+pi+zero%252Caps%252C227&amp;sr=8-2&_encoding=UTF8&tag=noma362907-22&linkCode=ur2&linkId=f2ce6310144d709312b4e5e14e19a7df&camp=247&creative=1211)

## Raspberry Pi 4 Model B 4GB

1. Discord bot (音楽・ラジオ再生) の常時稼働用、これは 3 でやってる時期もあった
2. Minecraft Server も起動できるものの MOD 無しでも最初から少しモッサリする
3. やったことないけど身近にやってる人がいた [地上波録画サーバ](https://bowmiow.net/garage/raspi-tv2/)、Mirakurun や EPGStation を使う
4. Nintendo Switch のコントローラ自作、4 で USB Gadget API が使える様になって可能になった。[スプラトゥーン3をマウスでプレイ ジャイロコンバーター [NXIC]](https://youtu.be/p048VY5oUCk?si=ex6EGEeFhgzXmXvq) ~~ただちょっとラグかったかな~~


## Raspberry Pi 5 8GB

Minecraft Server + 工業系MOD 3-4人で結構快適

スペック的に難しかった事が色々試せそう

[raspberry pi 5 購入リンク - amazon](https://www.amazon.co.jp/Raspberry-Development-Cortex-A76-quad-core-RAM%25EF%25BC%2589%25E3%2583%2592%25E3%2583%25BC%25E3%2583%2588%25E3%2582%25B7%25E3%2583%25B3%25E3%2582%25AF/dp/B0CQT288H2/ref=sr_1_5_pp?__mk_ja_JP=%25E3%2582%25AB%25E3%2582%25BF%25E3%2582%25AB%25E3%2583%258A&amp;crid=3J3T5LDZ74E63&amp;dib=eyJ2IjoiMSJ9.OBtTCTkPdbsi77Fp7vq1kPaFLPEDszaKRoCjQ7apwPgQr-0VO8OIW7B04s44ziT2u16Y3EYI1MJMWY8angixAd5uht_bJdbEqR5JOCSV6V39VcUch1SEZKwOyeqvyZO0Zln5t7QYtIVipenVFt3vrV1PBuCI-fpc-BrU3rWQImiqEWFertgaHftMEAzNatroBYo8nl16SsTvFn4-QeF6xM3YGDhU1KZvTkT0XPjyyl2Sau0QBM0Be61Fh980yW6WTWJmWtkXbZRLDEJqPxkgUjOCLlsF5pdCW9b-YaZ78iI.RjUGqi2lf0iUKaRW2Uy5ikIojT65LM5-dAf0N5LZJmI&amp;dib_tag=se&amp;keywords=raspberry+pi+5&amp;qid=1715473018&amp;sprefix=raspbeery+pi+%252Caps%252C176&amp;sr=8-5&_encoding=UTF8&tag=noma362907-22&linkCode=ur2&linkId=97c94075aaec1b55ed7449aa95875023&camp=247&creative=1211)

# 強みと弱み

## 強み

### 消費電力が少ない

大きい PC をずっと起動しておくと電気代が気になるので、何か常時稼働したい時はラズパイでできないかどうか考える様になりました。

### 安い

まえはもっと安かった気がするけれども・・・
ナンバリングが上がる毎にスペックは大幅に上がってるので、基本的に値段以外の理由で古いのを買う理由はないと思う。

## 弱み

### arm プロセッサに対応してないツールは使えない

例えば立てたいサーバーやアプリケーションに入れたライブラリが arm に対応していない場合、起動すらできないか、起動してもうまく動かない。
ただ arm に対応しているツールやライブラリは増えてきてるし、今後に期待。
また、box86 の様な x86 向けのツールを arm で動作させる エミュレータはある様子。

### 大容量なメモリのモデルがない

2024/5/12 時点だとラズパイ5が最新で最大メモリは 8GB みたい。
他の SBC の Rock5 だと 32GB モデルまであるみたいで、他のに目移り中。

### 電プチするとデータが破損する事がある

電源ケーブルぶっこぬきで電源をきるとデータが破損する事があります。
データの破損の仕方にもよりますが、何度か起動しなくなった経験があります。
すぐ壊れてしまうイメージを持ちそうですが、実際に↓の様な記事も多数あり、経験上も読み取り専用で運用していればその様な問題はおきませんでした。

[Raspberry Piは本当に壊れやすいのか](https://zenn.dev/su_/articles/97b9e25d0ae41c)
[Raspberry Pi OSのrootfs ROM 化 ― RAMディスク化しつつ、好きなパッケージを後から追加する方法](https://qiita.com/ma2shita/items/45818f0872472ecacac1)
[Raspberry PiのrootFSをROM化してSD Cardの破損を防ぐメモ](https://qiita.com/tomtwinkle/items/cb97bba8cd5c2748c30f)

電源ケーブルを抜いて電源を落とす様な運用がしたい場合、最低でも boot パーティションの読み取り専用は必要そうです。
