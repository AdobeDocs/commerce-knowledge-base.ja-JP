---
title: '''Magento-cloud'' [!DNL CLI]にアクティブな環境が表示されていません'
description: この記事では、「Magento-cloud」 [!DNL CLI] （コマンドラインツール）でアクティブな環境が表示されない既知のAdobe Commerceの問題について説明します。
feature: Cloud, Integration, Configuration
role: Developer
exl-id: 3c1b5de2-8888-4531-9dc1-cd478e3c96fc
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
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
