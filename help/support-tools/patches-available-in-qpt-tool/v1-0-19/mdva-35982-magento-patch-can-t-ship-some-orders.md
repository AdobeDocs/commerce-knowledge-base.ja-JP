---
title: 「MDVA-35982：一部の注文を出荷できない」
description: 特定の Web サイトに限定された管理者ユーザーが、同じ Web サイトで注文した商品の発送を作成できない場合は、MDVA-35982 パッチでエラーが修正されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.19 がインストールされている場合に利用できます。 パッチ ID は MDVA-35982。 この問題はAdobe Commerce 2.4.3 で修正されました。
exl-id: f41c6572-66bb-4697-93e3-da34b81829e2
feature: Orders, Shipping/Delivery
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# MDVA-35982：一部の注文を発送できません

特定の Web サイトに限定された管理者ユーザーが、同じ Web サイトで注文した商品の発送を作成できない場合は、MDVA-35982 パッチでエラーが修正されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.19 がインストールされている場合に使用できます。 パッチ ID は MDVA-35982。 この問題はAdobe Commerce 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

マーチャントは特定の注文を発送できません。

<u> 再現手順 </u>:

1. デフォルトストアを除く、商品の任意の製品 web サイトを選択します。 詳しい手順については、ユーザーガイドの [Web サイトの製品 ](https://docs.magento.com/user-guide/catalog/settings-basic-websites.html) を参照してください。
1. デフォルトの web サイト/ストアが選択されていないカスタムの役割範囲を使用して、管理者用のユーザーの役割を作成します。 詳細な手順については、ユーザーガイドの [ 役割の定義 ](https://docs.magento.com/user-guide/system/permissions-user-roles.html#define-a-role) を参照してください。
1. 編集モードで商品を開き、**詳細価格** でこの商品のグループ価格を設定します。 詳しい手順については、ユーザーガイドの [ グループ価格 ](https://docs.magento.com/user-guide/catalog/product-price-group.html) を参照してください。
1. この商品で注文を作成します。
1. このユーザーの役割で管理者としてログインし、出荷を作成します。 詳細な手順については、ユーザーガイドの [ 出荷の作成 ](https://docs.magento.com/user-guide/sales/shipments-create.html) を参照してください。

<u> 期待される結果 </u>:

出荷が作成されます。

<u> 実際の結果 </u>:

次のエラーが表示されます。

`"0":"Notice: Undefined offset: XX in \/vendor\/magento\/module-catalog\/Model\/Product\/Attribute\/Backend\/GroupPrice\/AbstractGroupPrice.php on line 290"`

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
