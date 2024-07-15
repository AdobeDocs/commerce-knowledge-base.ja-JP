---
title: ソースを削除したり、そのコードを変更したりできません
description: この記事では、ソースを完全に削除したり、コードを変更したりできない場合の解決策を提供します。
exl-id: dbdb4d62-9138-4a3d-a58f-8671f1dc5b42
feature: Console
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# ソースを削除したり、そのコードを変更したりできません

この記事では、ソースを完全に削除したり、コードを変更したりできない場合の解決策を提供します。

## 問題

製品の割り当てに関係なく、ソースを削除することはできません。

## 影響を受ける製品とバージョン

* Magentoインベントリがインストールされたクラウドインフラストラクチャー上のAdobe Commerce（すべてのバージョン）
* MagentoインベントリがインストールされたAdobe Commerce オンプレミス 2.3.0 以降
* Magento Open Source 2.3.0 以降（Magentoインベントリがインストールされている）

## 原因：

設計上、ソースを完全に削除したり、コードを変更したりすることはできません。

ソースを完全に削除すると、ソースは製品インベントリ、注文、出荷データなどの一部なので、注文データの問題が発生します。

コードは、ソースを注文に接続するために不可欠です。 これはソースの一意の ID で、編集できません。

## 解決策

在庫を移動するか、ある場所のすべての出荷から製品をドロップすることで、製品からソースを削除できます。

[SSA](https://devdocs.magento.com/guides/v2.3/inventory/source-selection-algorithms.html) 計算およびAdobe Commerce Inventory の受注処理からソースを削除する必要がある場合は、ソースを無効にできます。 無効にしたソースは、すべてのデータ、割り当てられた製品および在庫数量を保持し、いつでも再び有効にして再び出荷を開始できます。

ソースを無効にする方法について詳しくは、[ ソースの作成ガイド ](https://github.com/magento/inventory/wiki/Create-Sources#disable-sources) を参照してください。
