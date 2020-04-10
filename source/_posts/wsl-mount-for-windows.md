---
layout: post
title: WindowsからWSLのUbuntuのディレクトリをマウントする
date: 2020-02-11 22:46:44
tags: [wsl]
---

# 環境

- Windows10
- Ubuntu 18.04(WSL)

# 手順

## WSLのディレクトリを開く

実はエクスプローラからWSLのディレクトリを除くことが出来ます。

エクスプローラにて、\\\\wsl$を開く

![1](/images/wsl-mount-for-windows1.png)

## マウントしたいディレクトリを開き、アドレスをコピー

![2](/images/wsl-mount-for-windows2.png)

## マウント

「ネットワーク」を右クリックし、「ネットワークドライブの割り当て」を選択します。

![3](/images/wsl-mount-for-windows3.png)

その後、割り当てたいドライブレターを選択し、先ほどのアドレスを張り付けし、OKします。

![4](/images/wsl-mount-for-windows4.png)

## 確認

「PC」のツリー上に表示される様になります。

![5](/images/wsl-mount-for-windows5.png)

## アンマウント

![6](/images/wsl-mount-for-windows6.png)
