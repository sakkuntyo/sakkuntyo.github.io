---
layout: post
title: "[nodejs]プロジェクト内のパッケージをアップデート"
date: 2021-07-22 00:30:43
tags: [nodejs]
---

# 経緯
hexo が node v14 でうまく使えないのは hexo 3.9 が古すぎる事が原因の様で、
アップデートを試みました。

## 手順

### ncu コマンドをインストール
```
$ npm install npm-check-updates
```
必要に応じて -g をつけましょう

### ncu でアップデート
```
$ npx ncu -u
Upgrading /sakkuntyo.github.io/package.json
[====================] 16/16 100%

 hexo                                   ^3.9.0  →     ^5.4.0
 hexo-asset-link                        ^1.2.1  →     ^2.1.0
 hexo-deployer-git                      ^2.0.0  →     ^3.0.0
 hexo-directory-category                ^1.0.7  →     ^1.1.4
 hexo-generator-archive                 ^0.1.5  →     ^1.0.0
 hexo-generator-category                ^0.1.3  →     ^1.0.0
 hexo-generator-index                   ^0.2.1  →     ^2.0.0
 hexo-generator-seo-friendly-sitemap    0.0.25  →      0.2.1
 hexo-generator-tag                     ^0.2.0  →     ^1.0.0
 hexo-renderer-ejs                      ^0.3.1  →     ^1.0.0
 hexo-renderer-marked                   ^1.0.1  →     ^4.0.0
 hexo-renderer-stylus                   ^0.3.3  →     ^2.0.1
 hexo-server                            ^0.3.3  →     ^2.0.0
 netlify-cms                          ^2.10.13  →  ^2.10.148
```

hexo ブログ の プロジェクトだと上記の結果になった

### node_modules の再生成
```
$ rm -r node_modules/
$ npm i
```

### 正常に動くか試す
```
$ npx hexo server -D
```

![1](/images/nodejs-all-package-upgrade.png)

このプロジェクトの場合、まだまだ課題はあるみたいです。
恐らく使用しているテーマ Next が追従できていません。
