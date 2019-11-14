---
layout: post
title: Linuxの時間調整【Debian系OS】
date: 2019-11-15 01:02:43
tags: [Debian,Linux,timedatectl]
---

Windowsを入れている端末にLinuxをインストールすると、
RTCの時刻がLinuxに変更され、
Windowsで表示される時間がズレることがあります。
そんな時にいつも行う操作のメモ

## RTCとは

マザーボードが記憶した時刻です。
OSを起動した際にマザーボードから時刻が取得できる場合には、
まず最初にRTCの時刻を取得し、使用されます。


> *ポイント*
> インターネットに繋がる場合は、NTPを利用した時刻同期が行われます。
> インターネットにも繋がらず、RTCからの時刻取得もできない場合には、
> 以前シャットダウンした時刻を使用する事があります。(Ubuntu14,16,18で体験)

## 何故Windowsの時刻もズレてしまうのか

timedatectlコマンドを実行するとわかりますが、
Debianは少なくとも3つの時刻にアクセスし、それぞれの時刻を変更する事ができます。

```bash
$ timedatectl
                      Local time: 金 2019-11-15 01:28:34 JST
                  Universal time: 木 2019-11-14 16:28:34 UTC
                        RTC time: 木 2019-11-14 16:28:34
                       Time zone: Asia/Tokyo (JST, +0900)
       System clock synchronized: yes
systemd-timesyncd.service active: yes
                 RTC in local TZ: no
```

- Local Time(指定したタイムゾーンの時間)
- Universal Time(世界標準の時間、UTC)
- RTC Time(マザーボードの時間)

Linux(例えばUbuntu)を起動した際に、
RTCの時刻がUTC時刻等に合わされて調整されてしまうためです。

この記事を書いているのは日本時間(JST)でいうとAM 1:00ですが、
UTCでは9時間前の前日のPM 4:00となっています。

Linuxがデフォルトで持つ時間がUTCであり、
それを定期的にRTCに同期を行っているため、
次にWindowsを起動した場合に、「時刻がズレている」という状態になります。

## じゃあどうするのか

Linuxから２つの操作を行います。

- タイムゾーンを指定し、Local Timeを日本時間に変更
- Local TimeをRTCに同期する様に変更

## 手順

次の操作はLinux上で行います。

### 現在の時刻と設定を確認する

timedatectlコマンドを実行し、時刻を確認します。

```bash
$ timedatectl
                      Local time: 金 2019-11-15 16:28:34 UTC
                  Universal time: 木 2019-11-14 16:28:34 UTC
                        RTC time: 木 2019-11-14 16:28:34
                       Time zone: UTC (UTC, +0000)
       System clock synchronized: yes
systemd-timesyncd.service active: yes
                 RTC in local TZ: no
```

ここで確認したいのは

- タイムゾーン
- RTCへLocal Timeを同期するか

です。

タイムゾーンはUTC、RTCへLocal Timeを同期しない設定となっています。

そのため、次にWindowsを起動した際にはRTCの時刻がズレた状態となります。

### タイムゾーンをJSTにする

JSTとは日本時間の事です。

次のコマンドでタイムゾーンを日本時間に変更します。

```bash
$ timedatectl set-timezone Asia/Tokyo
```

念の為、設定が変わった事を確認します。

```bash
$ timedatectl
                      Local time: 金 2019-11-15 01:35:59 JST
                  Universal time: 木 2019-11-14 16:35:59 UTC
                        RTC time: 木 2019-11-14 16:35:59
                       Time zone: Asia/Tokyo (JST, +0900)
       System clock synchronized: yes
systemd-timesyncd.service active: yes
                 RTC in local TZ: no
```

### RTCに同期する時刻をLocal Timeにする

次のコマンドでRTCにLocal timeを同期させる設定を行います。

```bash
$ timedatectl set-local-rtc true
                      Local time: 金 2019-11-15 01:38:59 JST
                  Universal time: 木 2019-11-14 16:38:59 UTC
                        RTC time: 金 2019-11-15 01:38:59
                       Time zone: Asia/Tokyo (JST, +0900)
       System clock synchronized: yes
systemd-timesyncd.service active: yes
                 RTC in local TZ: yes

Warning: The system is configured to read the RTC time in the local time zone.
         This mode can not be fully supported. It will create various problems
         with time zone changes and daylight saving time adjustments. The RTC
         time is never updated, it relies on external facilities to maintain it.
         If at all possible, use RTC in UTC by calling
         'timedatectl set-local-rtc 0'.
```

何やら注意が出ていますが、Google翻訳をかけた所は以下の様なメッセージでした。

> 警告：システムは、ローカルタイムゾーンでRTC時間を読み取るように構成されています。
>       このモードは完全にはサポートできません。さまざまな問題が発生します
>       タイムゾーンの変更と夏時間の調整。 
>       RTC時間が更新されることはなく、外部の設備に依存して維持されます。
>       可能な場合は、UTCでRTCを使用して呼び出します
>       'timedatectl set-local-rtc 0'

ここでWindowsの時刻がズレない設定は完了です。

Ubuntu14,16,18とこの設定を使用していますが、今の所問題は見当たりません。

