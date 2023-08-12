---
layout: post
title: "Windows 11 の Hyper-V マシンに GPU を割り当てる(GPU-PV)"
date: 2023-07-21 00:00:00
tags: [GPU,GPU-PV,GPU-V]
---

GTX1080 から RTX 3090 に乗り換えたので、GPU-PV(旧名GPU-V) を改めて試してみようかなと
2020/11 頃に某ゲームを多重起動するために Windows 10 で実施していましたが、その時と手順は全く変わりませんでした。

# 現存する仮想マシンに GPU を使ってもらう方法

1. DDA
  - グラボが限定されます
2. Remote FX
  - 廃止済、今はできないはず
3. GPU-PV(旧名GPU-P)
  - 今回はコレ

# 前提

- ホストマシン
  - Windows 11 OSビルド 22621.1992
  - CPU: Ryzen9 3950X (16core/32threads)
  - GPU: RTX 3090
- ゲストマシン
  - Windows 11

# 手順
## 0. Hyper-V を実行するホストマシンでは事前に以下の設定をしておく
1. マザーボード側で VT-x または SR-IOV を有効化しておく
2. Windows 側で Hyper-V を有効化しておく(機能の有効化)

## 1. Hyper-V で Windows 11 マシンを作成する

## 2. ホスト側 で以下コマンドを実行

Windows 11 マシンを停止し、管理者権限で以下 PowerShell を実行

```
$MachinName="Hyper-V 上のマシン名"
Add-VMGpuPartitionAdapter -VMName "${MachinName}"
Set-VMGpuPartitionAdapter -VMName "${MachinName}" -MinPartitionVRAM 80000000 -MaxPartitionVRAM 100000000 -OptimalPartitionVRAM 100000000 -MinPartitionEncode 80000000 -MaxPartitionEncode 100000000 -OptimalPartitionEncode 100000000 -MinPartitionDecode 80000000 -MaxPartitionDecode 100000000 -OptimalPartitionDecode 100000000 -MinPartitionCompute 80000000 -MaxPartitionCompute 100000000 -OptimalPartitionCompute 100000000
Set-VM -GuestControlledCacheTypes $true -VMName "${MachinName}"
Set-VM -LowMemoryMappedIoSpace 1GB -VMName "${MachinName}"
Set-VM -HighMemoryMappedIoSpace 32GB -VMName "${MachinName}"
```

## 3. ホストマシンからゲストマシンへファイルをコピーする

ホストからのコピー元とゲストへのコピー先のパスが異なるので別々に記載、2つのファイルがあります。

以下の二つのファイルがコピー元

- 1. PowerShell で以下を実行すると出てくるフォルダ丸ごと
```
explorer.exe "$(Get-CimInstance -ClassName Win32_VideoController -Property * | Select-Object -ExpandProperty InstalledDisplayDrivers | Write-Output)".Split(",")[0].Trim("\nvldumdx.dll")
例: C:\WINDOWS\System32\DriverStore\FileRepository\nv_dispi.inf_amd64_50916785244854f2
```
- 2. C:\Windows\System32\nvapi64.dll

コピー先

- 1. C:\Windows\System32\HostDriverStore\FileRepository\ #HostDriverStore 以下のフォルダは自身で作成してください。
- 2. C:\Windows\System32\ #ホストと同じ場所

ここまで実施して再起動するとデバイスマネージャーに表示される
どこかに漏れがあるとビックリマークついてるかもしれません。

- うまくいった例
![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/708cfc42-4db9-4f95-a03d-e1de05d2f1b6)

- うまくいってない例
![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/9fb5bf88-ab77-4257-94b7-2e42c21e20ee)

# どんな感じ?

## ゲスト側のタスクマネージャでは GPU 表示されない

ゲスト側の使用率はゲスト側で見たかったんですけど見えず、0 % 表示

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/452c8eda-3333-4df8-900c-af96dcdcd6f9)

ただ FF14 ベンチが動作したので GPU は使えている様です

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/6290fd3d-3a9f-48f2-ac46-8eebe1020d47)

## ホスト側 FF14ベンチ (4K)

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/3de6f240-9355-4981-8d68-145f6bcdda04)

## ホスト側 FF14ベンチ (FullHD)

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/e8bf8e6a-7476-4e1f-b695-5a3a8a121a16)

## ゲスト側 FF14ベンチ (4K)

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/5696061f-fb6e-485e-a304-02cbbb8ff513)

## ゲスト側 FF14ベンチ (FullHD)

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/37358b6a-7eb8-4be8-8842-c760df63db21)

## ゲスト側 FF14ベンチ (4K)

- 設定値を少し変えた、わかりにくいですが、１桁あがっていたりしています。
```
Set-VMGpuPartitionAdapter -VMName "HyperVマシン名" -MinPartitionVRAM 1000000000 -MaxPartitionVRAM 1000000000 -OptimalPartitionVRAM 1000000000 -MinPartitionEncode 1000000000 -MaxPartitionEncode 1000000000 -OptimalPartitionEncode 100000000 -MinPartitionDecode 1000000000 -MaxPartitionDecode 1000000000 -OptimalPartitionDecode 1000000000 -MinPartitionCompute 1000000000 -MaxPartitionCompute 1000000000 -OptimalPartitionCompute 1000000000
```

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/c64c73ef-100b-4e1b-a0fe-a4cc66e2b45c)

- 20230725追記
設定値戻してもスコアがあがる事はありませんでした。何の差なんだ・・・

## Surface Laptop 3 (4K)
手元にあった Surface でもベンチしました。驚愕のスコア

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/a4a1e2ff-2db0-4878-a658-e03cd48ffcba)

## 体感

GPU-PV ないよりはいいかも、な感じ
-> 20230725追記: 6000くらい出ている時は結構いい

# 参考にしたサイト

- 今回↓見て思い出した。ハッ RTX 3090 にしてから試してなかった！
[Hyper-VでGPU(GPU-PV)を利用する方法 (Windows 10以降編)](https://qiita.com/Hyper-W/items/e189790fd4534d9d51ad)

- 2020年に↓見て試した、全く同じ手順だった。この時は GPU-P って名前だった、今書いていて気づいた、同じ人だった！
[Hyper-VでGPU(3Dアクセラレーション)を利用する方法 Windows 10以降編 (GPU-P)](https://qiita.com/Hyper-W/items/3a2c7ff1d983deb80070)

# おまけ

これを管理者権限有効 PowerShell で実行すると拡張セッション無し解像度4Kが使える様になる

```
Set-VMVideo -VMName "HyperVマシン名" -HorizontalResolution 3840 -VerticalResolution 2160 -ResolutionType Single
```
