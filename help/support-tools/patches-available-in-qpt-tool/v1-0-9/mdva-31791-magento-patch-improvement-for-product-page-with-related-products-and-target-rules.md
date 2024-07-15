---
title: 「MDVA-31791 パッチ：関連製品およびターゲットルールを使用した製品ページの改善」
description: '[ 関連製品 ] （https://docs.magento.com/user-guide/catalog/settings-advanced-related-products.html）または [ 関連製品ルール ] （https://docs.magento.com/user-guide/marketing/product-related-rules.html） （ターゲットルール）が使用されている場合、MDVA-31791 パッチにより製品ページのパフォーマンスが向上します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.9 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.1 で修正されました。'
exl-id: e737bccb-d9eb-4794-9d6b-2c22fa8edaa2
feature: Marketing Tools, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# MDVA-31791 パッチ：関連製品およびターゲットルールによる製品ページの改善

[](https://docs.magento.com/user-guide/catalog/settings-advanced-related-products.html) 関連製品）または [ 関連製品ルール ](https://docs.magento.com/user-guide/marketing/product-related-rules.html) （ターゲットルール）が使用される場合、MDVA-31791 パッチにより製品ページのパフォーマンスが向上します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.9 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.1 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用にパッチが作成されました。**

クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.4、2.3.4-p1、2.3.4-p2、2.4.0、2.4.0-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

関連製品または Target ルールを使用した場合、製品ページのパフォーマンスが低くなります。

[ 関連製品 ](https://docs.magento.com/user-guide/marketing/product-related-rules.html) または [ 関連製品ルール ](https://docs.magento.com/user-guide/catalog/settings-advanced-related-products.html) 機能を使用する場合は、MDVA 31791 ースのパッチの適用を検討してください。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
