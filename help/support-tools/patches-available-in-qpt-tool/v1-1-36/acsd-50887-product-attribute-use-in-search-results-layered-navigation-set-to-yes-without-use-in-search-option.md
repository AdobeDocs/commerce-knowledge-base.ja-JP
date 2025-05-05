---
title: 'ACSD-50887: *[!UICONTROL Use in Search Results Layered Navigation]* オプションを指定せずに、*[!UICONTROL Use in Search]*を Yes に設定する'
description: ACSD-50887 パッチを適用すると、Adobe Commerceの問題が修正されます。この問題では、*[!UICONTROL Use in Search]* オプションも*Yes*に設定されていない場合に、product 属性プロパティ*[!UICONTROL Use in Search Results Layered Navigation]*を*Yes*に設定できます。
feature: Attributes, Products, Search, Storefront
role: Admin, Developer
exl-id: b597709b-7489-41a0-b1ff-d68d0def0b46
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# ACSD-50887:*[!UICONTROL Use in Search]* オプションを指定せずに *[!UICONTROL Use in Search Results Layered Navigation]* を *はい* に設定する

ACSD-50887 パッチでは、*[!UICONTROL Use in Search]* オプションも *Yes* に設定されていない状態で、product 属性プロパティの *[!UICONTROL Use in Search Results Layered Navigation]* が *Yes* に設定される問題が修正されています。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.36 がインストールされている場合に使用できます。 パッチ ID は ACSD-50887 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.6-p2

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品属性プロパティ *[!UICONTROL Use in Search Results Layered Navigation]* は *はい* に設定できます。*[!UICONTROL Use in Search]* オプションも *はい* に設定する必要はありません。

これらの設定は、一緒に使用するように設計されています。 パッチを適用した状態で *[!UICONTROL Use in Search]* オプションを *いいえ* に設定すると、*[!UICONTROL Use in Search Results Layered Navigation]* オプションも *いいえ* に設定されているかのように機能します。

<u> 再現手順 </u>:

1. 管理者で、**[!UICONTROL Stores]** / **[!UICONTROL Attribute]** / **[!UICONTROL Product]** に移動し、複数選択タイプの属性を作成して、以下を設定します。

   * *[!UICONTROL Use in Search]= No*
   * *[!UICONTROL Use in Layered Navigation]= （任意のオプション）*
   * *[!UICONTROL Use in Search Results Layered Navigation]=はい*
   * *Name = Test_attribute*
   * *オプション*:
      * *ステッカー*
      * *ピッカー*

1. 新しい属性をデフォルトの属性セットに追加します。
1. 2 つの製品を作成します。

   1. 最初の製品：
      * 名前= ステッカー
      * 価格、数量、重量を 1 に設定
      * Test_attribute = select option *ステッカー*

   1. 2 番目の製品：
      * 名前= ピッカー
      * 価格、数量、重量を 1 に設定
      * Test_attribute =両方のオプションを選択します

1. 再インデックス `catalogsearch_fulltext` 実行します。

   `bin/magento indexer:reindex catalogsearch_fulltext`

1. 店頭で *ステッカー* という言葉で検索します。

<u> 期待される結果 </u>:

製品 *Sticker* のみが返されます。これは、*[!UICONTROL Use in Search]* が *No* に設定されている場合、[!DNL Elasticsearch] が Test_attribute のインデックスを作成しないためです。

<u> 実際の結果 </u>:

両方の製品が返されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
