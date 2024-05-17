---
title: '展開エラー：SQLSTATE[HY000]'
description: この記事では、SQLSTATE[HY000] エラーが原因でデプロイが失敗する問題の解決策を提供します。
exl-id: c6da6275-9327-4a5c-99ed-93a53952ba42
feature: Deploy
role: Developer
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# 展開エラー：SQLSTATE[000 HY]

この記事では、SQLSTATE が原因でデプロイが失敗する問題の解決策を提供します[000 HY] エラー。

## 影響を受ける製品とバージョン

* Adobe Commerce [すべてのデプロイメント方法](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

## 問題

展開中に SQLSTATE エラーが発生します。

```sql
Updating modules:
SQLSTATE[HY000]: General error: 23 Out of resources when opening file '/tmp/#sql_565c_0.MAD' (Errcode: 24 "Too many open files"),
```

## 原因：

デプロイ中に Cron を実行する。

## 解決策

この問題を解決するには、コマンドラインを開いて次のコマンドを実行して、cron が実行されていないことを停止します。
`./vendor/bin/ece-tools cron:disable`.
