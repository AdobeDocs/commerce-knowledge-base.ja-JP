---
title: Adobe AI 用に API キーを設定しましたが、1 つの SaaS データ領域しか表示されません
description: この記事では、Adobe AI の API キーを設定した後に、1 つの SaaS データ領域しか表示されない問題の解決策を説明します。
exl-id: e13041da-b122-4684-8287-42132931f47a
feature: REST, Saas, Observability
role: Developer
source-git-commit: 27b0836380c3040b26076b9cb81b9328cb2c9ff2
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Adobe AI 用に API キーを設定しましたが、1 つの SaaS データ領域しか表示されません

この記事では、Adobe AI の API キーを設定した後に、1 つの SaaS データ領域しか表示されない問題の解決策を説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法）：すべてのバージョン
* Magento Open Source：すべてのバージョン
* 拡張機能またはテクノロジー（Fastly、New Relicなど）、Adobe AI （Product Recommendations/Live Search）

## 問題

Adobe AI の API キーを設定しましたが、表示されるのは 1 つの SaaS データ領域のみです。

## 原因：

表示される SaaS データスペースの数は、Commerce ライセンスによって異なります。

* Adobe Commerce – 実稼動データスペース 1 つ、テスト用データスペース 2 つ
* Magento Open Source - 1 つの実稼動データスペース。テスト用のデータスペースは不要

## 解決策

* API キーがアカウント所有者のアカウントで作成されたことを確認します。 ユーザーのアカウントに共有アクセス権を付与され、自分のアカウントで鍵を作成した場合でも、これにより複数のデータスペースが付与されることはありません。
* アカウント所有者のアカウントでキーが生成された場合は、ライセンスが有効であること、つまり保留中の請求書がないことを確認します。
