---
title: 「MDVA-42969：関連製品ルールは、顧客セグメントが「すべて」に設定されている場合にのみ機能する」
description: MDVA-42969 パッチは、顧客セグメントが all に設定されている場合にのみ、関連する製品ルールが機能する問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.13 がインストールされている場合に利用できます。 パッチ ID は MDVA-42969。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 2877ba7a-2681-4de2-9c37-228de232424f
feature: Customer Service, Marketing Tools, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# MDVA-42969：関連製品ルールは、顧客セグメントが「すべて」に設定されている場合にのみ機能します

MDVA-42969 パッチは、顧客セグメントが all に設定されている場合にのみ、関連する製品ルールが機能する問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.13 がインストールされている場合に使用できます。 パッチ ID は MDVA-42969。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1 ～ 2.4.2-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

関連製品ルールは、顧客セグメントが「すべて」に設定されている場合にのみ機能します。

<u> 再現手順 </u>:

1. **ストア**/**設定**/**カタログ**/**ルールベースの商品関係** に移動し、**関連商品を表示** = **ルールベースのみ** を設定します。
1. **顧客**/**セグメント** に移動し、新しいセグメント **適用先** = **訪問者および登録済み顧客** を作成します。
1. **マーケティング**/**関連製品ルール** に移動して、新しいルールを作成します。

   ```code block
   Apply To = Related Products
   Customer Segments = All
   Products to Match = SKU = <select a SKU>
   Products to Display = SKU +is one of+ Constant Value (specify 1-3 products)
   ```

1. ストアフロントで一致する製品を開き、表示する製品が表示されていることを確認します。
1. 手順 3 で作成したルールを変更し、手順 2 から **顧客セグメント** = **特定** > **セグメント** に設定します。
1. ストアフロントで一致する製品を開きます。

<u> 期待される結果 </u>:

ルールベースの関連製品は、顧客セグメントが次の設定で作成されるので、製品の訪問者に対してストアフロントに表示されます。

**適用先** = **訪問者および登録済み顧客**

<u> 実際の結果 </u>:

関連製品は表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
