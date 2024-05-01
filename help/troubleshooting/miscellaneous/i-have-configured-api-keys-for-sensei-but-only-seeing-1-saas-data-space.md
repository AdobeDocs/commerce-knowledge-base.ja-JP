---
title: Senseiの API キーを設定しましたが、SaaS データ領域が 1 つしか表示されません
description: この記事では、Senseiの API キーを設定した後に、1 つの SaaS データ領域しか表示されない問題の解決策を説明します。
exl-id: e13041da-b122-4684-8287-42132931f47a
feature: REST, Saas, Observability
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# Senseiの API キーを設定しましたが、SaaS データ領域が 1 つしか表示されません

この記事では、Senseiの API キーを設定した後に、1 つの SaaS データ領域しか表示されない問題の解決策を説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法）：すべてのバージョン
* Magento Open Source：すべてのバージョン
* 拡張機能またはテクノロジー（Fastly、New Relicなど）、Adobe Sensei（製品Recommendations/ライブ検索）

## 問題

Senseiの API キーを設定しましたが、表示されるのは 1 つの SaaS データ領域のみです。

## 原因：

表示される SaaS データスペースの数は、Commerce ライセンスによって異なります。

* Adobe Commerce – 実稼動データスペース 1 つ、テスト用データスペース 2 つ
* Magento Open Source - 1 つの実稼動データスペースで、テスト用のデータスペースはない

## 解決策

* API キーがアカウント所有者のアカウントで作成されたことを確認します。 ユーザーのアカウントに共有アクセス権を付与され、自分のアカウントで鍵を作成した場合でも、これにより複数のデータスペースが付与されることはありません。
* アカウント所有者のアカウントでキーが生成された場合は、ライセンスが有効であること、つまり保留中の請求書がないことを確認します。
