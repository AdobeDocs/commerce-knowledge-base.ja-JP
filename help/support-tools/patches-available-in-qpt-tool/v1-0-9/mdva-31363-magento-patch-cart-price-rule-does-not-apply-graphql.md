---
title: 「MDVA-31363 パッチ：買い物かごの価格ルールが適用されない（GraphQL）」
description: MDVA-31363 パッチは、「買い物かご全体に対する固定金額割引」アクションが使用された場合に、クーポン付きの買い物かご価格ルールがGraphQL経由で適用されない問題を修正します。 このパッチは、Quality Patches Tool （QPT） 1.0.9 がインストールされている場合に使用できます。 この問題は、Adobe Commerce バージョン 2.4.2 で修正される予定です。
exl-id: f64fbbb1-b5fd-4624-bcdd-d1e6c1f9acfe
feature: GraphQL, Orders, Price Rules, Shopping Cart
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# MDVA-31363 パッチ：買い物かごの価格ルールが適用されない（GraphQL）

>[!WARNING]
>
>MDVA-33975 という新しいパッチは、GraphQLの価格計算の問題を修正します。 MDVA-31363 は非推奨であり、パッチ MDVA-33975 を適用することをお勧めします。 このパッチにアクセスするには、[MDVA-33975 パッチ：GraphQL price calculations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/patches/mdva-33975-magento-patch-graphql-price-calculations.html) を参照してください。

MDVA-31363 パッチは、「買い物かご全体に対する固定金額割引」アクションが使用された場合に、クーポン付きの買い物かご価格ルールがGraphQL経由で適用されない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.9 がインストールされている場合に使用できます。 この問題は、Adobe Commerce バージョン 2.4.2 で修正される予定です。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.2 - 2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

見積価格に関する応答を行う前に見積合計を再計算すると、適用されたルールが失われます。

<u> 再現手順 </u>:

1. シンプルな製品を作成します。
1. 買い物かご全体に対して固定金額割引の買い物かご価格ルールを作成します。
1. GraphQLを使用して、新しい買い物かごを作成します。
1. 応答から card\_id を保存し、GraphQLを使用して手順 1 の商品を買い物かごに追加します。
1. GraphQLを使用してクーポンコードを買い物かごに追加して、買い物かご価格ルールをアクティブ化します。
1. それに応じて価格を確認してください。

<u> 期待される結果 </u>:

割引が適用されます。

<u> 実際の結果 </u>:

割引は適用されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
