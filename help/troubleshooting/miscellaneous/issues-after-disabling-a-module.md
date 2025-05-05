---
title: モジュールを無効にした後の問題
description: この記事では、Commerce Admin でモジュール出力を無効にした後のモジュール機能の問題の解決策について説明します。
exl-id: 517f6993-f09e-4a94-8c57-175ecf9a98a8
feature: Extensions
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# モジュールを無効にした後の問題

この記事では、Commerce Admin でモジュール出力を無効にした後のモジュール機能の問題の解決策について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.1.X 以前のAdobe Commerce
* Adobe Commerce オンプレミス 2.1.X 以前

## 問題

Commerce管理でモジュール出力を無効にすると、**ストア**/**設定**/**設定**/詳細/**詳細** で、モジュール機能に関連する問題が発生する場合があります。

## 原因：

**Stores**/**Settings**/**Configuration**/ADVANCED/**Advanced** でモジュール出力を無効にすると、出力（HTML、JS）のみが無効になりますが、このモジュールの機能は無効になりません。

## 解決策

モジュール機能を無効にする必要がある場合は、アドビの開発者ドキュメントの [ モジュールの有効化または無効化 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/tutorials/manage-modules) の説明に従って、モジュールを無効にします。

モジュール出力の無効化機能は、バージョン 2.2.0 以降で削除されました。
