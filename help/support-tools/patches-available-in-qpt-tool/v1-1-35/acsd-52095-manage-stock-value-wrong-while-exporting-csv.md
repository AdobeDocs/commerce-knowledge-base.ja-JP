---
title: 「ACSD-52095:CSV の書き出し中に、在庫値の管理が間違っています」
description: CSV の書き出し中に商品の在庫管理方法で値が間違っていたAdobe Commerceの問題を修正するために、ACSD-52095 パッチを適用してください。
feature: Inventory, Products
role: Admin, Developer
exl-id: 9e599931-e9b1-4216-b78d-3993d9c3132d
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# ACSD-52095: [!UICONTROL Manage Stock] csv の書き出し中に値が正しくありません

ACSD-52095 パッチは、製品が存在する問題を修正します `manage_stock` csv の書き出し中に値が間違っています。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.35 がインストールされています。 パッチ ID は ACSD-52095 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.5-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

この `manage_stock` 製品の書き出し後、CSV ファイルの値が正しく 0 に設定されません。

<u>再現手順</u>:

1. に移動 **[!UICONTROL Admin]** > **[!UICONTROL Store]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Inventory]** > **[!UICONTROL Product Stock Options]** およびを設定 **[!UICONTROL Manage Stock]** = *[!UICONTROL No]*.
1. 新しい製品を作成して保存します。
1. に移動 **[!UICONTROL System]** > **[!UICONTROL Export]**.
1. を選択 *[!UICONTROL Entity Type]* = *[!UICONTROL Products]* 製品をエクスポートします。
1. 生成された CSV ファイルを確認します。 `manage_stock` = 0, `use_config_manage_stock` = 1。
1. 再び以下に移動 **[!UICONTROL Admin]** > **[!UICONTROL Store]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Inventory]** > **[!UICONTROL Product Stock Options]**、およびを設定  **[!UICONTROL Manage Stock]** = *[!UICONTROL Yes]*.
1. に移動 **システム** > **Export**.
を選択 *[!UICONTROL Entity Type]* = *[!UICONTROL Products and export the products]*.
1. 生成された CSV ファイルを確認します。 `manage_stock` = 0, `use_config_manage_stock` = 1。
1. 管理者で製品を開き、に移動します。 **[!UICONTROL Advanced Inventory]** を実行して、 **[!UICONTROL Manage Stock]** の値。

<u>期待される結果</u>

この **[!UICONTROL Manage Stock]** 値： *1* 製品に対して有効になっている場合。

<u>実際の結果</u>

この **[!UICONTROL Manage Stock]** 値： *0* 製品に対して有効になっている場合。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
