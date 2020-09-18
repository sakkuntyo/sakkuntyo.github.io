---
layout: post
title: NodejsのウェブサーバーでクライアントのIPを受け取る
date: 2020-09-19 01:09:55
tags: [nodejs]
---

# クライアントのIPを確かめたい！

そういう時はreqの情報をとる

```js
router.post('/webtest', function (req, res) {
  var reqdata = req.headers['x-forwarded-for'] || 
     req.connection.remoteAddress || 
     req.socket.remoteAddress ||
     req.connection.socket.remoteAddress;
  console.log(reqdata);
});
```
