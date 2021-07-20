---
layout: post
title: "Ryzen9 3950X を購入しました"
date: 2021-07-19 23:25:58
tags: [PC]
---

# 何故今更買ったのか

- 後述の良い所を持った CPU が \75000で手に入る + 会社から手当の出る対象商品になっていたので。
- とあるゲームをしていて複数起動 + マクロ操作をしたかったので。

![1](/images/3950X-siyoukan.jpg)

## 良い所

### 16 コア 32 スレッドの一般ユーザー向けCPU
サーバー向けのマザーボードを用意する必要がないので、
CPU以外のパーツに選定予知がまだまだあります。

### 安い

\75000です。これはかなり安い。
Intel の 16コアCPU の i9 9960X では \150000近くします。
しかも、i9 9960X では、サーバー向けのパーツが必要になります。
~~ただ、もう少しお金だして 5950X を購入してもよかったかも~~

### 強い

上記 Intel の 16コア CPU とベンチマークスコアの比較用

- AMD Ryzen9 3950X
![2](/images/3950X-siyoukan2.jpg)
https://www.cpubenchmark.net/cpu.php?cpu=AMD+Ryzen+9+3950X&id=3598

- Intel i9 9960X
![3](/images/3950X-siyoukan3.jpg)
https://www.cpubenchmark.net/cpu.php?cpu=Intel+Core+i9-9960X+%40+3.10GHz&id=3405

## 良くない所

### Nested Virtual Machine に非対応
強いマシンを持てば仮想マシンの中で仮想マシンを動作させたくなるものですが、
AMDのCPUの場合はまだ正式に対応していません。
※AMD でも Windows10 の Insider Preview バージョンを使用する事で可能です。

# 変更した構成

- M/B: MSI MAG B550 TOMAHAWK ※Ryzen5 1600X で使用していたマザーボードが非対応だったので
<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=noma362907-22&language=en_US&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B08B62MK65&linkId=56461ea1e7b746a3f2d018a28e87ac22"></iframe>
- CPU: AMD Ryzen9 3950X
<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=noma362907-22&language=en_US&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B07ZTYKLZW&linkId=5f1bea128e324a4265106ce091875a28"></iframe>
- メモリ: Patriot Viper Steel DDR4 3600MHz 32GB x 2 ※3000MHz 以下へのダウンクロックをする事で動作
<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=noma362907-22&language=en_US&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B08688GFPD&linkId=80130a81a8591587492798f4c5d9e62d"></iframe>

# 実際使ってみてどうか

マザーボードの変更が必要になった以外は、何も不便を感じませんでした。
HyperV を使用して、1コア1仮想マシンのスペックで 10個のマシンを動作させ、その中でゲームの実行もしましたが、
冒頭の画像にもありますが、CPU使用率は50手前くらい。
まだまだ、余裕を見せています。素直に買ってよかったです。

# どういう用途におすすめか

- PC スペックにロマンを求めたいけどちょっとコストも抑えたい人
- ゲームマクロ や RPA を並行実行したい人
