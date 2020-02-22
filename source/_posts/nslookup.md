---
layout: post
title: IPアドレスとドメインを正引、逆引する
date: 2020-02-22 15:48:57
tags: [cmd]
---

freenom等でドメインを入手、設定した際などに使う

# 環境

- Ubuntu 18.04 (Kagoya VPS)

# 正引きする（IPアドレスからドメインを確認）

```bash
$ nslookup 8.8.8.8
Server:         210.134.55.219
Address:        210.134.55.219#53

Non-authoritative answer:
8.8.8.8.in-addr.arpa    name = dns.google.

Authoritative answers can be found from:
8.8.8.in-addr.arpa      nameserver = ns3.google.com.
8.8.8.in-addr.arpa      nameserver = ns2.google.com.
8.8.8.in-addr.arpa      nameserver = ns4.google.com.
8.8.8.in-addr.arpa      nameserver = ns1.google.com.
ns1.google.com  internet address = 216.239.32.10
ns2.google.com  internet address = 216.239.34.10
ns4.google.com  internet address = 216.239.38.10
ns3.google.com  internet address = 216.239.36.10
ns1.google.com  has AAAA address 2001:4860:4802:32::a
ns2.google.com  has AAAA address 2001:4860:4802:34::a
ns4.google.com  has AAAA address 2001:4860:4802:38::a
ns3.google.com  has AAAA address 2001:4860:4802:36::a
```

# 逆引する（ドメインからIPアドレスを確認）

```bash
$ nslookup google.com
Server:         210.134.55.219
Address:        210.134.55.219#53

Non-authoritative answer:
Name:   google.com
Address: 216.58.199.238
```
