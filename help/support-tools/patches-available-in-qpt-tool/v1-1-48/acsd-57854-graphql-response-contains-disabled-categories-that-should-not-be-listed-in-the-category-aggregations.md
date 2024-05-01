---
title: 「ACSD-57854:*GraphQL*応答に、カテゴリ集計にリストされるべきでない無効なカテゴリが含まれています」
description: ACSD-57854 パッチを適用して、*GraphQL*応答に、カテゴリ集計にリストされるべきでない無効なカテゴリが含まれているAdobe Commerceの問題を修正してください。
feature: GraphQL
role: Admin, Developer
exl-id: b6130a0f-57bc-4719-99f2-beb630c463c7
source-git-commit: ea6f23a7ce599e24c6b683f82cf08b72b2506020
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# ACSD-57854: *GraphQL* 応答に、カテゴリ集計にリストされるべきではない、無効なカテゴリが含まれています

ACSD-57854 パッチは、 *GraphQL* 応答に、カテゴリ集計にリストすべきでない、無効なカテゴリが含まれています。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.48 がインストールされています。 パッチ ID は ACSD-57854 です。 この問題はAdobe Commerce 2.5.0 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

*GraphQL* 応答に、カテゴリ集計にリストすべきでない、無効なカテゴリが含まれています。

<u>再現手順</u>:

1. 2 つのカテゴリを作成します。
1. 商品（テストAdobe商品）を作成して、商品を両方のカテゴリに割り当てます。
1. 作成されたカテゴリの 1 つを無効にします。
1. 製品の使用 *GraphQL* 商品を検索します。
1. で製品カテゴリのリストを確認します。 *GraphQL* 応答。

<u>期待される結果</u>:

無効になっているカテゴリは、 *GraphQL* 応答。

<u>実際の結果</u>:

無効なカテゴリは、カテゴリ集計に一覧表示されます *GraphQL* 応答。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
