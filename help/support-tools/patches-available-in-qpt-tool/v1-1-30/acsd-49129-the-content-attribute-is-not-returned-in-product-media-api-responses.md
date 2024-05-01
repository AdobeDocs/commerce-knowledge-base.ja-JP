---
title: 「ACSD-49129：製品メディア API 応答で「Content」属性が返されない」
description: ACSD-49129 パッチを適用すると、「rest/V1/products/sku/media」 product media API 応答で*content*属性（*base64 image code*）が返されないAdobe Commerceの問題が修正されます。
exl-id: b7022046-3f52-4880-81b8-977ed270773f
feature: REST, Attributes, Media, Page Content, Products
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# ACSD-49129：製品メディア API 応答で「Content」属性が返されない

ACSD-49129 パッチは、 *コンテンツ* 属性（*[!UICONTROL base64 image code]*）は `rest/V1/products/sku/media` 製品メディア API の応答。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.30 がインストールされています。 パッチ ID は ACSD-49129 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.5-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

この *コンテンツ* 属性（*[!UICONTROL base64 image code]*）は `rest/V1/products/sku/media` 製品メディア API の応答。

<u>再現手順</u>:

1. 画像付きの製品を作成します。
1. 送信 *GET REST API* リクエスト先 `rest/V1/products/<sku>/media` および `rest/V1/products/<sku>/media/<entryId>`.
1. API の応答を確認します。

<u>期待される結果</u>

この *コンテンツ* データを含む属性は、REST API を介して利用できます。

<u>実際の結果</u>

この *コンテンツ* api 応答に属性がありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
