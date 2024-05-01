---
title: 'MDVA-33975 パッチ：GraphQLの価格計算'
description: 「MDVA-33975 パッチは、GraphQLの価格計算の問題を修正します。 その問題には、次のものが含まれます。'
exl-id: a8266334-72cb-4b50-9ff5-9a977d762e5c
feature: GraphQL, Customer Service, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# MDVA-33975 パッチ：GraphQLの価格計算

MDVA-33975 パッチは、GraphQLの価格計算の問題を修正します。 次に、問題の例を示します。

* カタログ価格ルールが特定の顧客グループに適用されると、買い物かごの商品価格と注文合計がGraphQLで正しく計算されません。
* カタログ価格ルールはに含まれていません `CartItemPrices` API 内で定義します。
* 一般顧客の顧客グループ価格は、GraphQLの商品クエリ応答に追加されません。
* 見積価格に関する応答を行う前に見積合計を再計算すると、適用されたルールが失われます。
* 最後の請求ステップで出荷金額割引が取得されず、総計が正しく表示されませんでした。
* 買い物かご価格ルール条件で顧客セグメントが使用されている場合、GraphQLでは割引が適用されません。

このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) v.1.0.14 がインストールされている。

## 影響を受ける製品とバージョン

* このパッチは、Adobe Commerce オンプレミス 2.4.1 用に設計されています。
* また、このパッチは、Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.4 ～ 2.4.1 のAdobe Commerce バージョンとも互換性があります。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
