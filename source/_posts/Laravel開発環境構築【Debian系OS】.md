---
title: Laravel開発環境構築【Debian系OS】
date: 2019-11-03 15:26:43
tags: [php]
---

## 前提環境

- Linux Mint19 Mate

## 手順

### phpをインストール

```bash
$ sudo apt update
$ sudo apt install -y php7.2 php7.2-mbstring php7.2-xml php7.2-gd php7.2-zip
$ sudo apt install -y sqlite3 php7.2-sqlite3 php7.2-mysql
$ php --version
$ php -m
```

### composerをインストール

```bash
$ curl -sS https://getcomposer.org/installer | php
$ sudo mv composer.phar /usr/local/bin/composer
$ sudo chmod +x /usr/local/bin/composer
$ composer --version
```

### Laravelをインストール

```bash
$ composer global require laravel/installer
```

### パスを通す

```bash
echo export PATH="~/.config/composer/vendor/bin:$PATH" >> ~/.bash_profile
source ~/.bash_profile
```
### 実際に起動しブラウザで確認

```bash
$ laravel new test
$ cd test
$ php artisan --version
$ php artisan serve --host 0.0.0.0
Laravel development server started: http://0.0.0.0:8000

```

ブラウザで接続してみると以下の様な画面が表示される

![laravel](/images/laravel-dev-create.png)

