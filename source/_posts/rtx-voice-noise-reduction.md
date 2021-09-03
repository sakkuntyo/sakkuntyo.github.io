---
layout: post
title: "ノイズキャンセルが可能な RTX Voice がすごい"
date: 2021-09-03 15:57:31
tags: ["audio"]
---

# ノイズキャンセルが可能なツール

## Krisp

他に知っているのは Krisp ですが、
こちらは基本有料。

しかし、Discord には Krisp が使える機能が搭載されているので、
Discord で使用する場合は特に難しい設定無く恩恵を受ける事が可能です。

https://krisp.ai/

## RTX Voice

https://www.nvidia.com/en-us/geforce/guides/nvidia-rtx-voice-setup-guide/

こちらは RTX グラフィックボードが搭載されている場合に使用可能なツールとして公開されました。
しかしながら、RTX グラフィックボードを必要とするため、利用要件が高かった様です。
ただ、GTX シリーズを搭載している場合にも使用可能な使用方法や、
GTX シリーズでも使用可能になったという情報があります。

- RTX Voiceがいつの間にかGTXでも動作するように！NVIDIAがシステム要件を緩和
https://www.nichepcgamer.com/archives/nvidia-rtx-voice-works-on-gtx-graphics-cards.html

また、こちらも、再生デバイスが再生する音のノイズキャンセルも可能です。

# 使い方

https://www.nvidia.com/en-us/geforce/guides/nvidia-rtx-voice-setup-guide/

1. 上記ページ内部の "For NVIDIA GeForce GTX GPUs, download RTX Voice." からダウンロードし、インストールする

2. RTX Voice の設定画面では、今現在使っているデバイスを選択しておく。

3. 通話時にデバイス選択ができないツールを使う場合には、RTX Voice を既定のデバイスにしておくことで使用可能。

# 注意

再生デバイスが再生する音のノイズキャンセルは特にいらなかったので、
サウンドコントロールパネルから、再生 の RTX Voice は無効化していました。
すると、次回以降RTX Voice の起動に失敗する様になるので、おすすめしません。
