---
title: '''Magento-cloud'' [!DNL CLI] にアクティブな環境が表示されない'
description: この記事では、「Magento-cloud」  [!DNL CLI]  （コマンドラインツール）でアクティブな環境が表示されない既知のAdobe Commerceの問題について説明します。
feature: Cloud, Integration, Configuration
role: Developer
exl-id: 3c1b5de2-8888-4531-9dc1-cd478e3c96fc
source-git-commit: 5eac8bb54e205eff6a96e279295cd12db1009f0a
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# `Magento-cloud` [!DNL CLI]にアクティブな環境が表示されていません

## イシュー

アクティブな環境がいくつかあり、`Magento-cloud` [!DNL CLI] （コマンドラインツール）コマンドを実行して、環境と対話しようとしています。 （例：`ssh`、`db:size`、`db:sql`など）
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

## 原因

デプロイメントが進行中、停止、または失敗したため、環境を利用できない可能性があります。

## Solution

環境を`e|-environment` フラグで手動で指定する必要があります。

1. アクティブな環境のリストを検索し、環境名をメモします。

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

&#x200B;2. 次のコマンドを使用して環境のIDを指定します。

`magento-cloud ssh -e integration`
