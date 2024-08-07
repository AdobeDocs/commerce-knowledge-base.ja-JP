---
title: 詳細検索ページの MDVA-28357 SKU 検索が機能しない
description: MDVA-28357 は、詳細検索ページで製品 SKU を検索しても、関連する製品が検索結果に表示されない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） v.1.0.8 がインストールされている場合に利用できます。 この問題は、Adobe Commerce バージョン 2.4.1 で修正されています。
exl-id: a89409b0-3155-4fac-9842-0d129dacd6e1
feature: Search
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# 詳細検索ページの MDVA-28357 SKU 検索が機能しない

MDVA-28357 は、詳細検索ページで製品 SKU を検索しても、関連する製品が検索結果に表示されない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) v.1.0.8 がインストールされている場合に使用できます。 この問題は、Adobe Commerce バージョン 2.4.1 で修正されています。

## 影響を受ける製品とバージョン

* このパッチは、Adobe Commerce オンプレミス 2.3.4-p2 用に設計されました。
* また、このパッチは、Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.0 ～ 2.3.5-p2 および 2.4.0 ～ 2.4.0-p1 とも互換性があります。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

詳細検索では、SKU を使用した検索では、ワイルドカードを使用して SKU フィールドがクエリされます。 ただし、ワイルドカードは `sku.keyword` でのみ使用できるので、予期された製品は返されません。

<u> 再現手順 </u>

1. 「詳細検索」ページに移動します。
1. SKU 番号で検索します。

<u> 実際の結果 </u>

*これらの検索条件に一致する項目が見つかりません。 検索を変更*.

<u> 期待される結果 </u>

次の検索条件を使用して *1 個の商品が見つかりました**SKU: XX-XXXX*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Quality Patches Tool を使用したパッチの適用 ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)。
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質パッチツールがリリースされました：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT ツールで使用可能なその他のパッチについては、[QPT ツールで使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
