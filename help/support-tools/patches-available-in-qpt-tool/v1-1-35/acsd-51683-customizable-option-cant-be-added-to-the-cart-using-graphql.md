---
title: 「ACSD-51683:GraphQLを使用してカスタマイズ可能なオプションを買い物かごに追加できない」
description: ACSD-51683 パッチを適用すると、GraphQLを使用してカスタマイズ可能なオプションを買い物かごに追加できないAdobe Commerceの問題を修正できます。
feature: GraphQL
role: Admin
exl-id: 4de0d8b7-714e-4bbf-8a0d-bb6e0c3aae55
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# ACSD-51683:GraphQLを使用してカスタマイズ可能なオプションを買い物かごに追加できない

ACSD-51683 パッチは、GraphQLを使用してカスタマイズ可能なオプションを買い物かごに追加できない問題を修正しました。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.35 がインストールされています。 パッチ ID は ACSD-51683 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

GraphQLを使用してカスタマイズ可能なオプションを買い物かごに追加することはできません。

<u>再現手順</u>:

1. カスタマイズ可能なでシンプルな製品を作成 **テキストフィールド** オプション。
1. [カートに追加](https://developer.adobe.com/commerce/webapi/graphql/tutorials/checkout/add-product-to-cart/) GraphQLから必要なカスタマイズ可能なオプションを使用して作成された商品。
1. を送信 [カート](https://developer.adobe.com/commerce/webapi/graphql/schema/cart/queries/cart/) GraphQLは、商品とその詳細をカートで確認するようにリクエストします。

<u>期待される結果</u>

この `Customizable_options` GraphQL応答の「」セクションには、商品を買い物かごに追加する際に提供されたデータが含まれています。

<u>実際の結果</u>

この `Customizable_options` GraphQL応答の「」セクションが空です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
