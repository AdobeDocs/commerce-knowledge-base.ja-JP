---
title: 不明なモジュール Magento_BundleSampleData
description: この記事では、Adobe Commerceのインストール中に発生した不明なモジュールエラーの修正について説明します。
exl-id: c927bc8f-d70b-4305-87c1-223001212555
feature: Extensions
role: Developer
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# 不明なモジュール Magento_BundleSampleData

この記事では、Adobe Commerceのインストール中に発生した不明なモジュールエラーの修正について説明します。

## 問題 {#details}

インストール中に、次のようなメッセージが表示されます。

```text
[ERROR] exception 'LogicException' with message 'Unknown module in the requested list: 'Magento_BundleSampleData''
```

## 解決策 {#solution}

次の各操作を一度に実行してから、インストールを再試行してください。

1. Web セットアップ ウィザードを実行します。 モジュールのリストは次のとおりです  **高度なモジュール設定**. を無効にするには **Magento\_BundleSampleData** モジュールで、 **Magento\_BundleSampleData** チェックボックスを選択します（下図を参照）。

   ![tshoot_bundlesampledata.png](assets/tshoot_bundlesampledata.png)

1. Web ブラウザーからすべてのブラウザー履歴とデータを消去します。
1. Chrome がある場合は、サイトに関連するすべてのブラウザーデータを消去します。  に移動 **設定** > **詳細オプション** > **プライバシー** > **コンテンツ設定** > **すべての cookie とサイトデータ**. 「サイト」列で、Adobe Commerce サーバーのアドレスをクリックし、 **すべて削除**.
