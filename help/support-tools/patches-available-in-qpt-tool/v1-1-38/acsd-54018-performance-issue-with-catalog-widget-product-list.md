---
title: 「ACSD-54018：カタログウィジェットの製品リストに関するパフォーマンスの問題」
description: ACSD-54018 パッチを適用すると、条件と属性タイプがブール値のカタログウィジェットの商品リストを追加する際に、ページの読み込みに時間がかかるAdobe Commerceの問題を修正できます。
feature: Attributes, Catalog Management, Page Builder, Page Content, Storefront
role: Admin, Developer
exl-id: 9f20484d-58c7-49d8-87df-1eeb84bee6fe
source-git-commit: dccb8dde1666fa0c72c7c94cd94c82daddaadc54
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# ACSD-54018：カタログウィジェットの製品リストに関するパフォーマンスの問題

ACSD-54018 パッチでは、条件と属性タイプがブール値のカタログウィジェットの製品リストを追加すると、ページの読み込みに時間がかかる問題を修正しました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.38 がインストールされている場合に使用できます。 パッチ ID は ACSD-54018 です。 この問題はAdobe Commerce 2.4.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.5-p4

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

条件と属性タイプがブール値のカタログウィジェットの製品リストを追加すると、ページの読み込みに時間がかかる。

<u> 再現手順 </u>:

1. 100,000 個の製品を生成。
1. スコープが [!UICONTROL Store View] に設定された bool 属性を作成します。
1. 属性をすべての属性セットに割り当てます。
   * すべての製品に属性値 *はい* を割り当てます。
1. **[!UICONTROL Catalog]**/**[!UICONTROL Products]** に移動し、100,000 個の製品をすべて選択します。
   * **[!UICONTROL Actions]** > **[!UICONTROL Update Attribute]** を選択します。
   * bool 属性を *はい* に設定して保存します。
   * この手順でログアウトした場合は、*メモ* を確認します。
1. CLI に移動し、`php bin/magento queue:con:start product_action_attribute.update` を実行します。
   * すべての製品の属性が更新されていることを確認します。
1. **[!UICONTROL Content]**/**[!UICONTROL Pages]** に移動して、新しいページを作成します。
1. **[!UICONTROL Page Builder]**/**[!UICONTROL Add row]**/**[!UICONTROL Add Content]**/**[!UICONTROL Products]** を開きます。
1. *[!UICONTROL Select Products By]* = *[!UICONTROL Condition]* を選択します。
1. 条件 *[!UICONTROL Created attribute]* を *[!UICONTROL Yes]* に設定して保存します。
1. フロントエンドに移動し、作成したページを開きます。
1. フルページキャッシュを無効にし、HTML キャッシュをブロックします。
1. ページ読み込み速度を確認します。
1. ページを数回再読み込みし、平均読み込み時間を計算します。

<u> 期待される結果 </u>:

ページの読み込みが速くなります。

<u> 実際の結果 </u>:

ページの読み込みに 5～10 秒かかります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
