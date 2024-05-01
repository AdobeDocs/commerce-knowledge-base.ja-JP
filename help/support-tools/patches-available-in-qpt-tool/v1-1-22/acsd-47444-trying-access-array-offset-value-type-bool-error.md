---
title: '''ACSD-47444: _[!UICONTROL Trying to access array offset on value of type bool]_ PHP 7.4 上の既知の製品に対して存在しない特定のカテゴリパスにアクセスするとエラーが発生する'
description: ACSD-47444 パッチを適用して、_があるAdobe Commerceの問題を修正します[!UICONTROL Trying to access array offset on value of type bool]_ PHP 7.4 で、既知の製品の存在しないカテゴリパスにアクセスするとエラーが発生する。
exl-id: dfe803d0-bcff-40e6-a759-8c2243235ea8
feature: Categories, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# ACSD-47444: _[!UICONTROL Trying to access array offset on value of type bool]_php 7.4 上で既知の製品に対して存在しない特定のカテゴリパスにアクセスする際にエラーが発生する

ACSD-47444 パッチは、以下に示す問題を解決します _[!UICONTROL Trying to access array offset on value of type bool]_php 7.4 上で既知の製品に対して存在しない特定のカテゴリパスにアクセスする際にエラーが発生します。このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.22 がインストールされています。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.2-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

次のエラーが発生します。 _[!UICONTROL Trying to access array offset on value of type bool]_php 7.4 上で既知の製品の存在しないカテゴリパスにアクセスする場合。

<u>前提条件</u>:

PHP 7.4

<u>再現手順</u>:

1. 「test」という名前で新しい製品を作成します。
1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL CATALOG]** > **[!UICONTROL Catalog]** > **[!UICONTROL Search Engine Optimization]** > 設定 **[!UICONTROL Generate "category/product" URL Rewrites]** = _不可_.
1. ストアフロントに移動して、../abc/test.htmlのような URL にアクセスします（「abc」は存在しないでください）。

<u>期待される結果</u>:

404 ページ。

<u>実際の結果</u>:

500 エラー：

_[!UICONTROL Notice: Trying to access array offset on value of type bool in /app/code/Magento/CatalogUrlRewrite/Model/Storage/DynamicStorage.php on line 182]_

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) 開発者向けドキュメントを参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
