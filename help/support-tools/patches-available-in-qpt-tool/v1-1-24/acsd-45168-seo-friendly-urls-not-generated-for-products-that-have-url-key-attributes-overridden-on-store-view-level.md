---
title: 「ACSD-45168:url_key 属性が上書きされた製品で、SEO に対応する URL が生成されない」
description: ACSD-45168 パッチを適用すると、ストアビューレベルで url_key 属性が上書きされた商品に対して SEO に対応する URL が生成されないAdobe Commerceの問題が修正されます。
exl-id: cdba42ac-3c96-439b-befa-f0a13587b5d9
feature: Attributes, Cache, Categories, Marketing Tools, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# ACSD-45168:url_key 属性が上書きされた製品で、SEO に対応する URL が生成されない

ACSD-45168 パッチでは、ストアビューレベルで url_key 属性が上書きされた製品で、SEO に対応する URL が生成されない問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.24 がインストールされています。 パッチ ID は ACSD-45168 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ストアビューレベルで url_key 属性が上書きされている製品については、SEO に対応する URL は生成されません。

<u>再現手順</u>:

1. に移動して、次のように設定します。 **[!UICONTROL Commerce Admin]** > **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Search Engine Optimization]**:
   * [!UICONTROL Use Categories Path for Product URLs] = *はい*
   * [!UICONTROL Generate "category/product" URL Rewrites] = *はい*
1. 設定キャッシュをクリーンアップします。
1. 2 つのカテゴリを作成します。 [!UICONTROL Category 1] および [!UICONTROL Category 2].
1. 2 つの製品を作成します。 [!UICONTROL Product 1] 。対象： [!UICONTROL Category 1], [!UICONTROL Product 2] 。対象： [!UICONTROL Category 1].
1. 範囲をに変更します。 [!UICONTROL Default Store View] （用） [!UICONTROL Product 1].
1. オプションの URL をオフにする [!UICONTROL Key] 。対象： [!UICONTROL Search Engine Optimization].
1. 商品を保存します。
1. 切り替え先 [!UICONTROL All Store Views].
1. 追加 [!UICONTROL Product 1] 対象： [!UICONTROL Category 2]を追加し、 [!UICONTROL Product 2] 対象： [!UICONTROL Category 2].
1. を確認します [!UICONTROL url_rewrite] テーブルまたは [!UICONTROL Marketing] > [!UICONTROL SEO & Search] > [!UICONTROL URL Rewrites].

<u>期待される結果</u>:

の SEO に対応する URL [!UICONTROL Category 2] の作成対象 [!UICONTROL Product 1].

<u>実際の結果</u>:

の SEO に対応する URL [!UICONTROL Category 2] ががありません [!UICONTROL Product 1] ストア表示範囲の URL キー属性が上書きされていたためです。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
