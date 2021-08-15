---
layout: post
title: "[Azure] kusto クエリをテスト実行する"
date: 2021-08-15 19:21:14
tags: [Azure,kusto]
---

# Details
Application Insights や Log Analytics ワークスペースにログが全く収集されていない状況でも、
１クエリ内でテーブルとログの定義を行い、
任意のデータが存在する事を想定し、クエリをテスト実行する事が出来ます。

## テーブルとログの定義を行うクエリ
```
datatable (Date:datetime, Event:string)
    [datetime(1910-06-11), "Born",
     datetime(1930-01-01), "Enters Ecole Navale",
     datetime(1953-01-01), "Published first book",
     datetime(1997-06-25), "Died"]
```

上記クエリを使用する事でリソース内のログデータの有無に関わらず、検索結果に表示する事ができます。
![1](/images/azure-kusto-query-execution-test.jpg)

## 使用例
### 比較演算子 !~ ってどんな挙動になるか調べたい
以下の様なクエリを実行する事で確認できます。

#### 検証１
- クエリ
```
datatable (Date:datetime, Event:string)
    [datetime(1910-06-11), "Born",
     datetime(1930-01-01), "Enters Ecole Navale",
     datetime(1953-01-01), "Published first book",
     datetime(1997-06-25), "Died"]
| where Event !~ "born"
```

- 結果
![1](/images/azure-kusto-query-execution-test2.jpg)



#### 検証２
- クエリ
```
datatable (Date:datetime, Event:string)
    [datetime(1910-06-11), "Born",
     datetime(1930-01-01), "Enters Ecole Navale",
     datetime(1953-01-01), "Published first book",
     datetime(1997-06-25), "Died"]
| where Event !~ "Born"
```

- 結果
![1](/images/azure-kusto-query-execution-test3.jpg)

## Log Analytics のデモ環境

実はサンプルのログが入っている環境も用意されています。ここでも色々テストできそう
https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring_Logs/DemoLogsBlade
