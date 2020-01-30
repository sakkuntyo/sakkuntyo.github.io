---
layout: post
title: Hexoでsitemap.xmlを生成する
date: 2020-01-30 23:41:11
tags: [Hexo,sitemap.xml]
---

Google検索エンジンの検索に出すために、
記事を追加する度にサーチコンソールにURLを登録していました、
sitemap.xmlを登録する事で、都度登録する必要がなくなります。

# 手順

## sitemap.xml生成プラグインをインストール

```bash
$ npm install hexo-generator-seo-friendly-sitemap --save
package.jsonをgitに追加します
$ git add package.json
```

## _config.ymlに追記

以下の行をHexoプロジェクト直下の_config.ymlに追記する事で、
hexo generate時にsitemapが作成される様になります。

```yaml
sitemap:
  path: sitemap.xml
```

hexo generateをしてみます

```bash
$ hexo generate
INFO  Start processing
INFO  Files loaded in 614 ms
INFO  Generated: post-sitemap.xml
INFO  Generated: sitemap.xml
INFO  Generated: tag-sitemap.xml
INFO  Generated: index.html
INFO  5 files generated in 1.14 s
```

今回幾つかsitemapが作成された事がわかります。

- post-sitemap.xml
  - 記事毎のページが記載されたsitemap
- tag-sitemap.xml
  - タグ毎のページが記載されたsitemap
- sitemap.xml
  - 内容見てもよくわからない(?)

## sitemapをサーチコンソールに登録

sitemapの登録は[ここ](https://search.google.com/search-console/sitemaps)から行えます。

登録に失敗する場合は、
_config.ymlに記述しているURL部分が間違っている可能性があります。
このURLはデプロイ後にアクセスするページのURLを指定しておく必要があります。

以下例
```
url: https://sakkuntyo.github.io
```
