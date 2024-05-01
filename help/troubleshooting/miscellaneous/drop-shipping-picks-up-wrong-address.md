---
title: ドロップシッピングは間違った住所を拾う
description: 配送ソリューションは、商品の発送元の住所を受け取りません。
exl-id: ce89713f-d506-4e4f-bf49-cdee3e6d29b5
feature: Customer Service, Orders, Shipping/Delivery
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# ドロップシッピングは間違った住所を拾う

## 問題

配送ソリューションは、商品の発送元の住所を受け取りません。

## 影響を受ける製品とバージョン

* Magentoインベントリがインストールされたクラウドインフラストラクチャー上のAdobe Commerce（すべてのバージョン）
* MagentoインベントリがインストールされたAdobe Commerce オンプレミス 2.3.0 以降
* Magento Open Source 2.3.0 以降（Magentoインベントリがインストールされている）

### 原因：

Magento在庫は現在、チェックアウト時の発送元住所に基づく直接配送料計算の使用をサポートしていません。 代わりに、設定のデフォルトのストアアドレスがすべての場合に使用されます。

## 関連資料

* [Magentoインベントリに関するよくある質問](https://github.com/magento/inventory/wiki/MSI-FAQs) （GitHub 内）。
