---
title: 「MDVA-28300:GraphQLのカタログ価格ルールに関する価格計算の問題」
description: MDVA-28300 パッチは、GraphQL リクエストがカタログ価格ルールからの価格変更を反映しない問題を修正します。 このパッチは、Quality Patches Tool （QPT） v.1.0.6 がインストールされている場合に使用できます。 この問題は、Adobe Commerce バージョン 2.3.6 で修正されました。
exl-id: 86079d29-db69-4758-a159-aeed8e0ea21f
feature: Catalog Management, GraphQL, Customer Service, Marketing Tools, Orders, Price Rules
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# MDVA-28300:GraphQLのカタログ価格ルールに関する価格計算の問題

>[!WARNING]
>
>MDVA-33975 という新しいパッチは、GraphQLの価格計算の問題を修正します。 MDVA-28300 は非推奨であり、パッチ MDVA-33975 を適用することをお勧めします。 このパッチにアクセスするには、を参照してください。 [MDVA-33975:GraphQLの価格計算](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/patches/mdva-33975-magento-patch-graphql-price-calculations.html).

MDVA-28300 パッチは、GraphQL リクエストがカタログ価格ルールからの価格変更を反映しない問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) v.1.0.6 がインストールされている。 この問題は、Adobe Commerce バージョン 2.3.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** Adobe Commerce オンプレミス 2.3.5-p1

**Adobe Commerce バージョンとの互換性：** cloud infrastructure 2.3.0 - 2.3.5-p2 上のAdobe Commerce オンプレミスとAdobe Commerce

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カタログ価格ルールが特定の顧客グループに適用されると、買い物かごの商品価格と注文合計がGraphQLで正しく計算されません。

<u>再現手順：</u>

1. 新しい顧客アカウントを作成し、その顧客グループを Wholesale に変更します。
1. に新しいカタログルールを作成する **Marketing** > **プロモーション** > **カタログ価格ルール** 次のパラメーターを使用します。
   * 顧客グループ：WholesaleActions:
   * 適用： *オリジナルのパーセンテージとして適用*
   * 割引： *50*


1. 価格=100 の新製品を作成します。
1. 以前に作成した顧客アカウントを使用してフロントエンドにログインします（既にログインしている場合は、ログアウトしてから再度ログインします）。
1. 商品を買い物かごに追加します。 製品の価格は 50 （通常価格 100）で、注文合計：55 （出荷原価の 50 + 5）。
1. に記載されているGraphQL API 呼び出しを実行します。 [customerCart クエリ](https://devdocs.magento.com/guides/v2.3/graphql/queries/customer-cart.html) 開発者向けドキュメントを参照してください。

<u>期待される結果：</u>

API とフロントエンドの両方が同じ注文合計を持ち、カタログルールによって導入された割引が適用されます。

<u>実際の結果：</u>

注文の合計には、カタログルールの割引は適用されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [品質向上パッチツールを使用したパッチの適用](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html).
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html).

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、QPT で使用可能なパッチの節を参照してください。
