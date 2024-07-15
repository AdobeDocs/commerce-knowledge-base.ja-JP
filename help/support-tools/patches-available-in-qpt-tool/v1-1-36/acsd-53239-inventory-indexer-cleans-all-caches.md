---
title: 「ACSD-53239：インベントリインデクサーがすべてのキャッシュをクリーンアップする」
description: ACSD-53239 パッチを適用して、インベントリインデクサーが [!UICONTROL Update on Schedule] モードですべてのキャッシュをクリーンアップするAdobe Commerceの問題を修正してください。
feature: GraphQL, Inventory, Catalog Management
role: Admin, Developer
exl-id: b8e68cf7-d326-4c9e-8749-d83113de2070
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# ACSD-53239: インベントリインデクサーが [!UICONTROL Update on Schedule] モードですべてのキャッシュをクリーンアップします

ACSD-53239 パッチでは、インベントリインデクサーが [!UICONTROL Update on Schedule] モードですべてのキャッシュをクリーンアップする問題が修正されています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.36 がインストールされている場合に使用できます。 パッチ ID は ACSD-53239 です。 この問題はAdobe Commerce 2.4.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.5-p4

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

インベントリインデクサーは、[!UICONTROL Update on Schedule] モードですべてのキャッシュをクリーンアップします。

<u> 再現手順 </u>:

1. **[!UICONTROL Admin]**/**[!UICONTROL Catalog Products]** に移動して、「約 *1200*」製品を選択します。
2. *[!UICONTROL Qty]* を新しい値に更新し、「**[!UICONTROL Save]**」をクリックします。
3. 保存直後に `bin/magento cron:run` を実行します。
4. 次のGraphQL クエリを実行します。

   ```GraphQL
   {
     storeConfig {
     absolute_footer
     }
   }
   ```

<u> 期待される結果 </u>

クエリは通常の時間内に処理されます。

<u> 実績 </u>

クエリの処理に異常な時間がかかる。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
