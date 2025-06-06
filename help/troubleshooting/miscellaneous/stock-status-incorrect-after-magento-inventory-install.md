---
title: Inventory managementのインストール後に、在庫ステータスが正しくない
description: この記事では、Inventory managementのインストール/アップグレード後に在庫ステータスが正しくなくなる問題を修正します。
exl-id: ae32fbe3-deab-4f31-b427-95f8b54a476f
feature: Install, Inventory, Orders
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# Inventory managementのインストール後に、在庫ステータスが正しくない

この記事では、Inventory managementのインストール/アップグレード後に在庫ステータスが正しくなくなる問題を修正します。

## 一部のサイトで在庫状況が不正確です

複数の web サイトを含むAdobe Commerce環境でInventory managementを使用するには、最初にをインストールまたはアップグレードを行った後で、必ずしもすべての web サイトの商品の在庫ステータスが適切になるわけではありません。

## 影響を受ける製品とバージョン

* Inventory managementがインストールされたクラウドインフラストラクチャー上のAdobe Commerce（すべてのバージョン）
* Inventory managementがインストールされているAdobe Commerce オンプレミス 2.3.0 以降
* Inventory managementがインストールされているMagento Open Source 2.3.0 以降

## 原因：

最初にインストールまたはアップグレードすると、すべての製品がデフォルトのソースに割り当てられ、すべての数量がそのソースに関連付けられます。 デフォルトのSourceは、関連付けられたデフォルトの web サイトを使用して、デフォルトの在庫に割り当てられます。

## 解決策

複数の web サイトがある場合は、これらの web サイトをSales Channelとしてデフォルト在庫または他のカスタム在庫に追加する必要があります。

これを行う方法について詳しくは、ユーザーガイドの wiki/ユーザーガイドの [Stock の節 ](https://experienceleague.adobe.com/ja/docs/commerce-admin/inventory/stocks/stocks-manage) を参照してください。
