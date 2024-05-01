---
title: 「ACSD-53239：インベントリインデクサーがすべてのキャッシュをクリーンアップする」
description: ACSD-53239 パッチを適用して、インベントリインデクサーがのすべてのキャッシュをクリーンアップするAdobe Commerceの問題を修正してください [!UICONTROL Update on Schedule] モード。
feature: GraphQL, Inventory, Catalog Management
role: Admin, Developer
exl-id: b8e68cf7-d326-4c9e-8749-d83113de2070
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# ACSD-53239：インベントリインデクサーが [!UICONTROL Update on Schedule] モード

ACSD-53239 パッチでは、インベントリインデクサーが内のすべてのキャッシュをクリーンアップする問題が修正されています。 [!UICONTROL Update on Schedule] モード。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.36 がインストールされています。 パッチ ID は ACSD-53239 です。 この問題はAdobe Commerce 2.4.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.5-p4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

インベントリインデクサーは、 [!UICONTROL Update on Schedule] モード。

<u>再現手順</u>:

1. に移動 **[!UICONTROL Admin]** > **[!UICONTROL Catalog Products]** 「about」を選択します。 *1200* 製品。
2. 更新 *[!UICONTROL Qty]* を新しい値に変更し、 **[!UICONTROL Save]**.
3. 実行 `bin/magento cron:run` 保存直後。
4. 次のGraphQL クエリを実行します。

   ```GraphQL
   {
     storeConfig {
     absolute_footer
     }
   }
   ```

<u>期待される結果</u>

クエリは通常の時間内に処理されます。

<u>実際の結果</u>

クエリの処理に異常な時間がかかる。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
