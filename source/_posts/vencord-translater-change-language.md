---
layout: post
title: "vencord の translater プラグインで英語以外の言語に翻訳させる"
date: 2023-09-27 00:00:00
tags: [discord]
---

# vencord ってなに
以前から改造版 Discord クライアントとして主流な BetterDiscord がありましたが、
最近出てきた(私が見かける様になった)新しい 改造版 Discord クライアントです。

# 導入方法
ここを見て Discord PTB をインストールし、Discord PTB に Vencord を適用しました。Canary も前に入れてるので、3ついれてる。

[【BetterDiscord超え】新改造版Discord、"Vencord"の入れ方とおすすめプラグイン - その1](https://unicode.hatenablog.jp/entry/vencord)

Vencord を導入したら 設定 > Plugins から Translater を有効化しましょう。

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/40ec9123-6825-435f-a679-96d7ac2ab709)


# あれ、日本語にならない。。。

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/dd887822-0523-4825-a636-61e50948bb64)

# 日本語に翻訳させる方法

プラグインを有効化する時に設定画面を開くこともできるのですが、ここには変換先の言語を選べる所がないんですよね。。。

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/4c224a41-fa9f-4b43-b05f-7e71cc07da67)

でも、プラグインのソースコードを漁っていたらなんだか変更できたりしちゃいそうな書き方になっている。

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/3af950c6-ac5d-4623-8d94-6e617c76484c)

色々みていた結果、設定 > Plugin の画面で変更しているのはこのファイルの様でした。

%appdata%\Vencord\settings\settings.json

translate の設定部分も見つかったので見てみると、ありました。

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/6584b704-f202-470f-8ecf-0c94c2fff348)

receivedOutput を ja にして保存しましょう。

```json
        "Translate": {
            "enabled": true,
            "autoTranslate": false,
            "receivedInput": "auto",
            "receivedOutput": "ja"
        },
```

また、英語の発言を右クリックして translate すると、できた。

![image](https://github.com/sakkuntyo/sakkuntyo.github.io/assets/20591351/290c5e03-ddba-4ccd-b5f1-61929b97d576)

