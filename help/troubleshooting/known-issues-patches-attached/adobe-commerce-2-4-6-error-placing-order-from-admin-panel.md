---
title: 管理パネルからのAdobe Commerce 2.4.6 エラー
description: この記事では、Commerce管理パネルから注文した後、ストアの選択でスタックした場合の、cloud infrastructure 2.4.6 での既知のAdobe Commerceの問題に対するパッチを提供します。
feature: Admin Workspace
role: Developer
exl-id: b30be5a5-3681-41db-9040-3624faed7c46
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# 管理パネルからのAdobe Commerce 2.4.6 エラー

この記事では、Commerce管理パネルから注文した後、ストアの選択でスタックした場合の、cloud infrastructure 2.4.6 での既知のAdobe Commerceの問題に対するパッチを提供します。

## 問題

管理パネルから注文を行うと、ストアの選択が行き詰まります。

<u> 再現手順 </u>

1. **[!UICONTROL Sales]**/**[!UICONTROL Orders]** に移動し、注文を作成する顧客を選択します。
2. 店舗セレクター画面から注文する店舗を選択します。

<u> 期待される結果 </u>

ストアを選択したら、注文を完了できます。

<u> 実際の結果：</u>

ストアを選択すると、ストアセレクターページにリダイレクトされ、注文を作成できなくなります。

## パッチ

次のリンクをクリックして、パッチをダウンロードします。

[ACSD-52277_2.4.6.patch のダウンロード](assets/ACSD-52277_2.4.6.patch.zip)

### 互換性のあるAdobe Commerce バージョン

このパッチは、Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.4.6 および 2.4.6-p1 用に作成され、これらのバージョンと互換性があります。

## パッチの適用方法

* クラウドインフラストラクチャー上でAdobe Commerceにパッチを適用する方法については、クラウドインフラストラクチャー上のCommerce ガイドの [ パッチの適用 ](/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) を参照してください。
* オンプレミスでAdobe Commerceにパッチを適用する方法については、アドビのCommerce アップグレードガイドの [ パッチの適用 ](/docs/commerce-operations/upgrade-guide/patches/apply.html?lang=en#composer) を参照してください。
