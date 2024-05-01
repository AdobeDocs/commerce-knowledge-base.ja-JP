---
title: 「Magento雲」 [!DNL CLI] はアクティブな環境を表示しません
description: この記事では、「Magentoクラウド」という既知のAdobe Commerceの問題について説明します [!DNL CLI] （コマンドラインツール）アクティブな環境は表示されません。
feature: Cloud, Integration, Configuration
role: Developer
exl-id: 3c1b5de2-8888-4531-9dc1-cd478e3c96fc
source-git-commit: 5eac8bb54e205eff6a96e279295cd12db1009f0a
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# この `Magento-cloud` [!DNL CLI] はアクティブな環境を表示しません

## 問題

いくつかのアクティブな環境があり、 `Magento-cloud` [!DNL CLI] （コマンドラインツール）コマンド。 （例： `ssh`, `db:size`, `db:sql`等）
ただし、目的の環境を選択するプロンプトには、この環境は表示されません。 （例：統合環境）

```
Enter a number to choose an environment:
Default: master
  [0] integration2 (type: development)
  [1] master (type: development)
  [2] production
  [3] staging
 >
```

## 原因：

デプロイメントが進行中、停止、または失敗したため、環境が利用できない場合があります。

## 解決策

を使用して、環境を手動で指定する必要があります。 `e|-environment` フラグ。

1. アクティブな環境のリストを見つけて、環境名をメモします。

```
$ magento-cloud environment: list |grep "Active\|ID"
Your environments are:

| ID                     | Title            | Status       | Type           |
| Master                 | Master           | Active       | Development    |
|   Production           | Production       | Active       | Production     |
|     Staging            | Staging          | Active       | Staging        |
|       Integration      | Integration      | Active       | Development    |
|          Integration 2 | Integration 2    | Active       | Development    |
```

2. コマンドを使用して環境の ID を指定します。

`magento-cloud ssh -e integration`
