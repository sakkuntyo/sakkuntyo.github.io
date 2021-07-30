---
layout: post
title: curlで出力を消す、繰り返す
date: 2021-07-31 01:13:02
tags: [linux]
---

Webサーバーの負荷を高くした検証をする時などに

# 例

## 出力を消す
```
$ curl -s -o /dev/null https://***.com
```

## 繰り返す
```
$ while [ 1 == 1 ];do curl https://***.com;done
```

## キャッシュを使わない
```
$ while [ 1 == 1 ];do curl -H 'Cache-Control: no-cache' https://***.com;done
```

## 出力を消して繰り返し、キャッシュは使わない
```
$ while [ 1 == 1 ];do curl -s -o /dev/null -H 'Cache-Control: no-cache' https://***.com;done
```

## 出力を消して繰り返し、キャッシュは使わずバックグラウンド実行
```
$ while [ 1 == 1 ];do curl -s -o /dev/null -H 'Cache-Control: no-cache' https://***.com;done &
```

何度も何度も実行するとその分多くリクエストが行われる。
