---
title: 「ACSD-44938：ゲストユーザーのGraphQL リクエストで VAT_ID を適用できない」
description: ACSD-44938 パッチは、ゲストユーザーのGraphQL リクエストで VAT_ID を適用できない問題を修正しました。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.18 がインストールされている場合に利用できます。 パッチ ID は ACSD-44938 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: 18b3dfa5-b666-491e-a067-526a53294f39
feature: Admin Workspace, GraphQL
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# ACSD-44938: ゲストユーザーのGraphQL リクエストで VAT_ID を適用できません

ACSD-44938 パッチは、ゲストユーザーのGraphQL リクエストで VAT_ID を適用できない問題を修正しました。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.18 がインストールされています。 パッチ ID は ACSD-44938 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.3-p3

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ゲストユーザーのGraphQL リクエストには VAT_ID を適用できません。

<u>再現手順</u>:

1. に記載されている手順に従います [GraphQL チュートリアル](https://devdocs.magento.com/guides/v2.4/graphql/tutorials/checkout/checkout-shopping-cart.html) 開発者向けドキュメントの「ゲスト用カートの作成」を参照してください。
1. GraphQLを使用して、ゲストユーザーに VAT_ID を適用してみてください。

<u>期待される結果</u>:

VAT_ID は、登録済みの顧客と同じ方法で適用できます。 参照： [createCustomerAddress ミューテーション](https://devdocs.magento.com/guides/v2.4/graphql/mutations/create-customer-address.html) 開発者向けドキュメントの記事。

<u>実際の結果</u>:

GraphQLを使用しているゲストユーザーに VAT_ID を適用することはできません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
