---
layout: post
title: "curl で chatgpt 3.5 を試す"
date: 2023-04-02 02:00:00
tags: [ai,chatgpt]
---

記事の更新の仕方すら忘れてしまいそうだったので何か書きこんどこうかなと

# curl コマンド

```
curl https://api.openai.com/v1/chat/completions -H "Content-Type: application/json" -H "Authorization: Bearer トークン" -d @- <<EOF
{
  "model":"gpt-3.5-turbo-0301",
  "messages": [{"role":"user","content":"こんにちは"}],
  "temperature":0.7
}
EOF
```

# ドキュメント
https://platform.openai.com/docs/guides/chat
