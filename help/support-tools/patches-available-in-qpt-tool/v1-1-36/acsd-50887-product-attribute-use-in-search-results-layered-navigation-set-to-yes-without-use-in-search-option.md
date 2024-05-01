---
title: 'ACSD-50887: *[!UICONTROL Use in Search Results Layered Navigation]*を除いてはいに設定する*[!UICONTROL Use in Search]* オプション'
description: ACSD-50887 パッチを適用して、product 属性プロパティ *が存在するAdobe Commerceの問題を修正してください[!UICONTROL Use in Search Results Layered Navigation]*は、*なしで*はい*に設定できます[!UICONTROL Use in Search]* オプションも*Yes*に設定されています。
feature: Attributes, Products, Search, Storefront
role: Admin, Developer
exl-id: b597709b-7489-41a0-b1ff-d68d0def0b46
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# ACSD-50887: *[!UICONTROL Use in Search Results Layered Navigation]* をに設定 *はい* なし *[!UICONTROL Use in Search]* オプション

ACSD-50887 パッチは、製品属性プロパティが *[!UICONTROL Use in Search Results Layered Navigation]* はに設定できます。 *はい* なし *[!UICONTROL Use in Search]* オプションも次のように設定されています *はい*. このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.36 がインストールされています。 パッチ ID は ACSD-50887 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.6-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品属性プロパティ *[!UICONTROL Use in Search Results Layered Navigation]* はに設定できます。 *はい* なし *[!UICONTROL Use in Search]* オプションも次のように設定されています *はい*.

これらの設定は、一緒に使用するように設計されています。 パッチを適用した状態で、 *[!UICONTROL Use in Search]* オプションの設定 *不可*, *[!UICONTROL Use in Search Results Layered Navigation]* オプションは、次のように機能するように非表示になっています *不可*.

<u>再現手順</u>:

1. 管理者で、に移動します。 **[!UICONTROL Stores]** > **[!UICONTROL Attribute]** > **[!UICONTROL Product]** さらに、multiselect タイプの属性を作成し、以下を設定します。

   * *[!UICONTROL Use in Search]=いいえ*
   * *[!UICONTROL Use in Layered Navigation]= （任意のオプション）*
   * *[!UICONTROL Use in Search Results Layered Navigation]=はい*
   * *名前= Test_attribute*
   * *オプション*:
      * *ステッカー*
      * *ピッカー*

1. 新しい属性をデフォルトの属性セットに追加します。
1. 2 つの製品を作成します。

   1. 最初の製品：
      * 名前= ステッカー
      * 価格、数量、重量を 1 に設定
      * Test_attribute = オプションを選択 *ステッカー*

   1. 2 番目の製品：
      * 名前= ピッカー
      * 価格、数量、重量を 1 に設定
      * Test_attribute =両方のオプションを選択します

1. 実行 `catalogsearch_fulltext` 再インデックス：

   `bin/magento indexer:reindex catalogsearch_fulltext`

1. 単語で検索 *ステッカー* 店先で。

<u>期待される結果</u>:

商品のみ *ステッカー* が返されるのは、 [!DNL Elasticsearch] 次の場合、Test_attribute のインデックスを作成しない *[!UICONTROL Use in Search]* はに設定されています。 *不可*.

<u>実際の結果</u>:

両方の製品が返されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
