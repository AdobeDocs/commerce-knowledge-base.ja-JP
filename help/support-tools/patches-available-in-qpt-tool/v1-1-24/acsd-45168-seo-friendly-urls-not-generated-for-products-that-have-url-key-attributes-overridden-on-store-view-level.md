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

ACSD-45168 パッチでは、ストアビューレベルで url_key 属性が上書きされた製品で、SEO に対応する URL が生成されない問題が修正されています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.24 がインストールされている場合に使用できます。 パッチ ID は ACSD-45168 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.5-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ストアビューレベルで url_key 属性が上書きされている製品については、SEO に対応する URL は生成されません。

<u> 再現手順 </u>:

1. **[!UICONTROL Commerce Admin]**/**[!UICONTROL Stores]**/**[!UICONTROL Settings]**/**[!UICONTROL Configuration]**/**[!UICONTROL Catalog]**/**[!UICONTROL Search Engine Optimization]** に移動して、次のように設定します。
   * [!UICONTROL Use Categories Path for Product URLs] = *はい*
   * [!UICONTROL Generate "category/product" URL Rewrites] = *はい*
1. 設定キャッシュをクリーンアップします。
1. [!UICONTROL Category 1] と [!UICONTROL Category 2] の 2 つのカテゴリを作成します。
1. [!UICONTROL Category 1] に [!UICONTROL Product 1]、[!UICONTROL Category 1] に [!UICONTROL Product 2] という 2 つの製品を作成します。
1. [!UICONTROL Product 1] の範囲を [!UICONTROL Default Store View] に変更します。
1. [!UICONTROL Search Engine Optimization] のオプションの URL [!UICONTROL Key] のチェックを外します。
1. 商品を保存します。
1. [!UICONTROL All Store Views] に戻ります。
1. [!UICONTROL Product 1] を [!UICONTROL Category 2] に追加し、[!UICONTROL Product 2] を [!UICONTROL Category 2] に追加します。
1. [!UICONTROL url_rewrite] テーブルまたは [!UICONTROL Marketing]/[!UICONTROL SEO & Search]/[!UICONTROL URL Rewrites] を確認します。

<u> 期待される結果 </u>:

[!UICONTROL Category 2] の SEO に対応する URL が [!UICONTROL Product 1] 用に作成されます。

<u> 実際の結果 </u>:

[!UICONTROL Category 2] の SEO に対応した URL が、ストア表示範囲の URL キー属性で上書きされていたため、[!UICONTROL Product 1] にありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
