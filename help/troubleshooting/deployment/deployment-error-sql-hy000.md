---
title: デプロイメントエラー：SQLSTATE[HY000]
description: この記事では、SQLSTATE[HY000] エラーが原因でデプロイメントが失敗する問題の解決策を提供します。
exl-id: c6da6275-9327-4a5c-99ed-93a53952ba42
feature: Deploy
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 5%
---
# デプロイメントエラー：SQLSTATE[HY000]

この記事では、SQLSTATE[HY000] エラーが原因でデプロイメントが失敗する問題の解決策を提供します。

## 影響を受ける製品とバージョン

* Adobe Commerce、[すべてのデプロイメント方法](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

## イシュー

デプロイメント中にSQLSTATE エラーが発生します。

```sql
Updating modules:
SQLSTATE[HY000]: General error: 23 Out of resources when opening file '/tmp/#sql_565c_0.MAD' (Errcode: 24 "Too many open files"),
```

## 原因

デプロイメント中に実行するCron。

## Solution

この問題を解決するには、コマンドラインを開いて次のコマンドを実行して、cronの実行を停止します。
`./vendor/bin/ece-tools cron:disable`.
