---
layout: post
title: Linux でのディスクベンチマーク
date: 2024-05-16
tags: [Linux]
---

ラズパイで nvme を gen3 で認識させるかそうでないかで速度がどれくらい変わるのか確認のために使いました

# コマンド

```
dd if=/dev/zero of=./test bs=1M count=10240 status=progress;rm test
```

10 GB 分書き込んで測定します。

Windows の CrystalDiskMark で測定した時の SEQ1M の項目と大体同じ事をしてるのだろう、と思ってます。

# ラズパイでの実行結果例

ラズパイでは /boot/firmware/config.txt の dtparam を nvme にするか、pciex1_gen=3 にするかで gen3 で認識するかどうかが変わるみたいです。

## dtparam=nvme

```
$ dd if=/dev/zero of=./test bs=1M count=10240 status=progress;rm test
10480517120 bytes (10 GB, 9.8 GiB) copied, 23 s, 456 MB/s
10240+0 records in
10240+0 records out
10737418240 bytes (11 GB, 10 GiB) copied, 23.484 s, 457 MB/s
```

## dtparam=pciex1_gen=3

```
$ dd if=/dev/zero of=./test bs=1M count=10240 status=progress;rm test
10410262528 bytes (10 GB, 9.7 GiB) copied, 13 s, 801 MB/s
10240+0 records in
10240+0 records out
10737418240 bytes (11 GB, 10 GiB) copied, 13.3776 s, 803 MB/s
```

ちゃんと早くなってる事が確認できました。
