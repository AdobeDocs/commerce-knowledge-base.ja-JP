---
title: 'ACSD-47444:_[!UICONTROL Trying to access array offset on value of type bool]_ PHP 7.4 上の既知の製品に対して、存在しない特定のカテゴリパスにアクセスするとエラーが発生する'
description: PHP 7.4 上で既知の商品に対して存在しない特定のカテゴリパスにアクセスする際に_[!UICONTROL Trying to access array offset on value of type bool]_ エラーが発生するAdobe Commerceの問題を修正するために、ACSD-47444 パッチを適用してください。
exl-id: dfe803d0-bcff-40e6-a759-8c2243235ea8
feature: Categories, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# ACSD-47444: PHP 7.4 上の既知の製品に対して存在しない特定のカテゴリパスにアクセスすると _[!UICONTROL Trying to access array offset on value of type bool]_&#x200B;エラーが発生する

ACSD-47444 パッチを適用すると、PHP 7.4 上の既知の製品に対して存在しない特定のカテゴリパスにアクセスする際に _[!UICONTROL Trying to access array offset on value of type bool]_&#x200B;のエラーが発生する問題が解決されます。このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.22 がインストールされている場合に使用できます。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.2-p2

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

PHP 7.4 で、既知の製品に対して存在しない特定のカテゴリパスにアクセスすると、_[!UICONTROL Trying to access array offset on value of type bool]_&#x200B;というエラーが発生します。

<u> 前提条件 </u>:

PHP 7.4

<u> 再現手順 </u>:

1. 「test」という名前で新しい製品を作成します。
1. **[!UICONTROL Stores]**/**[!UICONTROL Settings]**/**[!UICONTROL Configuration]**/**[!UICONTROL CATALOG]**/**[!UICONTROL Catalog]**/**[!UICONTROL Search Engine Optimization]**/set **[!UICONTROL Generate "category/product" URL Rewrites]** = _No_ に移動します。
1. ストアフロントに移動して、../abc/test.htmlのような URL にアクセスします（「abc」は存在しないでください）。

<u> 期待される結果 </u>:

404 ページ。

<u> 実際の結果 </u>:

500 エラー：

_[!UICONTROL Notice: Trying to access array offset on value of type bool in /app/code/Magento/CatalogUrlRewrite/Model/Storage/DynamicStorage.php on line 182]_

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
