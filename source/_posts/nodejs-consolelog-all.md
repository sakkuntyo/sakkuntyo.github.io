---
layout: post
title: "[nodejs]request body の中身を全て表示"
date: 2021-07-19 00:00:00
tags: [nodejs]
---

# リクエストボディの中身を全て表示する

Azure Monitor のアラートのjsonペイロードを取得する時などに

```js
router.post('/webtest', function (req, res) {
  console.dir(JSON.stringify{req.body});
  //その他処理
});
```
