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

ACSD-54018 パッチでは、条件と属性タイプがブール値のカタログウィジェットの製品リストを追加すると、ページの読み込みに時間がかかる問題を修正しました。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.38 がインストールされています。 パッチ ID は ACSD-54018 です。 この問題はAdobe Commerce 2.4.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.5-p4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

条件と属性タイプがブール値のカタログウィジェットの製品リストを追加すると、ページの読み込みに時間がかかる。

<u>再現手順</u>:

1. 100,000 個の製品を生成。
1. スコープがに設定された bool 属性を作成します。 [!UICONTROL Store View].
1. 属性をすべての属性セットに割り当てます。
   * 属性値の割り当て *はい* を全製品に適用します。
1. 次に進む **[!UICONTROL Catalog]** > **[!UICONTROL Products]**&#x200B;を選択し、100,000 個の製品をすべて選択します。
   * を選択 **[!UICONTROL Actions]** > **[!UICONTROL Update Attribute]**.
   * bool 属性をに設定します。 *はい* 保存します。
   * この手順でログアウトした場合は、 *備考*.
1. CLI に移動し、を実行します。 `php bin/magento queue:con:start product_action_attribute.update`.
   * すべての製品の属性が更新されていることを確認します。
1. 次に進む **[!UICONTROL Content]** > **[!UICONTROL Pages]** 新しいページを作成します。
1. 開く **[!UICONTROL Page Builder]** > **[!UICONTROL Add row]** > **[!UICONTROL Add Content]** > **[!UICONTROL Products]**.
1. を選択 *[!UICONTROL Select Products By]* = *[!UICONTROL Condition]*.
1. 条件を設定 *[!UICONTROL Created attribute]* 対象： *[!UICONTROL Yes]* 保存します。
1. フロントエンドに移動し、作成したページを開きます。
1. フルページキャッシュを無効にし、HTML キャッシュをブロックします。
1. ページ読み込み速度を確認します。
1. ページを数回再読み込みし、平均読み込み時間を計算します。

<u>期待される結果</u>:

ページの読み込みが速くなります。

<u>実際の結果</u>:

ページの読み込みに 5～10 秒かかります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
