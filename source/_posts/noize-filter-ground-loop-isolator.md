---
layout: post
title: "ノイズフィルターを試してみた"
date: 2022-05-05 02:00:00
tags: [Audio]
---

# 何でノイズフィルター？
OBS を使った配信環境を整えていますが、スマブラや太鼓の達人をやるときに遅延があると不利(太鼓の達人に至っては結構シビア)
な事がわかったので、OBS 上やソフトウェア上の映像を見ずに、モニターに映した画面を収録することにしました。
モニターのイヤホンジャックから、ミニプラグで音を取り、オーディオミキサーでPCの音とゲームの音を結合してみると、モニターからの音にノイズが乗っていました。(あるあるなんですけどね。)

## そこでこうしました

![old-haisinkankyou](https://user-images.githubusercontent.com/20591351/166729626-5f014e63-c7e4-4c77-8f52-1885d58f9385.png)

![sin-haisinkankyou](https://user-images.githubusercontent.com/20591351/166729691-b907fee8-eed0-439d-9107-b46c3c7473bd.png)

## 導入したノイズフィルター

<a href="https://www.amazon.co.jp/SmofG01/dp/B0171PQLB8?crid=24ELHZU98U787&keywords=%E3%82%B0%E3%83%A9%E3%83%B3%E3%83%89%E3%83%AB%E3%83%BC%E3%83%97%E3%82%A2%E3%82%A4%E3%82%BD%E3%83%AC%E3%83%BC%E3%82%BF%E3%83%BC&qid=1651679384&s=musical-instruments&sprefix=%E3%82%B0%E3%83%A9%E3%83%B3%E3%83%89%E3%83%AB%E3%83%BC%E3%83%97%E3%81%82%E3%81%84%E3%81%9D%E3%82%8C%E3%83%BC%E3%81%9F%E3%83%BC%2Cmi%2C172&sr=1-1-spons&psc=1&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUExUFgxOTBQWkNSUUozJmVuY3J5cHRlZElkPUEwNTEwMjM5MzJSWFY2TjNHT0VESiZlbmNyeXB0ZWRBZElkPUExOE5NWFhQSDBNUEc2JndpZGdldE5hbWU9c3BfYXRmJmFjdGlvbj1jbGlja1JlZGlyZWN0JmRvTm90TG9nQ2xpY2s9dHJ1ZQ%3D%3D&linkCode=li2&tag=noma362907-22&linkId=41245459b0c17de09975900b9cfc88b3&language=en_US&ref_=as_li_ss_il" target="_blank"><img border="0" src="//ws-fe.amazon-adsystem.com/widgets/q?_encoding=UTF8&ASIN=B0171PQLB8&Format=_SL160_&ID=AsinImage&MarketPlace=JP&ServiceVersion=20070822&WS=1&tag=noma362907-22&language=en_US" ></a><img src="https://ir-jp.amazon-adsystem.com/e/ir?t=noma362907-22&language=en_US&l=li2&o=9&a=B0171PQLB8" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />

## フェライトコアも試したが、、、効果無し

Sound Engine で音量を見ながらテストしましたが、フェライトコア (6ターン) はほとんど効果がありませんでした。

### ノイズ対策 - なし
![taisaku-nasi](https://user-images.githubusercontent.com/20591351/166723939-0a4709b3-13f3-44d6-99dd-7065ad47fbba.png)


### ノイズ対策 - フェライトコア 6 ターン
![taisaku-feraitocore](https://user-images.githubusercontent.com/20591351/166723956-022fc521-4ce7-4ccb-ad3d-69e0730f2ab3.png)


### ノイズ対策 - グランドループアイソレーター
![taisaku-grandloopisolator](https://user-images.githubusercontent.com/20591351/166723950-9a7c9535-4968-427f-9f5a-df675aa663af.png)

## このノイズの原理について調べた

逆流&ループが起きる場合があるそうです。
この動画を見て、なんとなく理解ができました。

![image](https://user-images.githubusercontent.com/20591351/166733692-bed21083-12bf-40f9-a34c-ad6e6f222833.png)
> https://www.youtube.com/watch?v=arYvWHUuX_Y
