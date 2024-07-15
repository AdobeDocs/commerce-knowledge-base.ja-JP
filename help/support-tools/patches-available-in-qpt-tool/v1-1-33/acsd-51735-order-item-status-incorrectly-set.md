---
title: 「ACSD-51735：製品在庫が 0 の場合、注文項目のステータスが誤って*[!UICONTROL Ordered]*に設定される」
description: 商品の在庫が 0 の場合に注文商品のステータスが誤って*[!UICONTROL Ordered]*に設定されるAdobe Commerceの問題を修正するには、ACSD-51735 パッチを適用してください。
feature: Orders, Products
role: Admin
exl-id: c6376698-71dc-46b8-a5b2-86dc26a574ab
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# ACSD-51735：製品在庫が 0 の場合、注文項目のステータスが誤って *[!UICONTROL Ordered]* に設定される

製品の在庫が 0 の場合に、注文項目のステータスが誤って *[!UICONTROL Ordered]* に設定される問題が ACSD-51735 パッチで修正されました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.33 がインストールされている場合に使用できます。 パッチ ID は ACSD-50895 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.4-p4

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品在庫が 0 の場合、注文項目のステータスが正しく *[!UICONTROL Ordered]* に設定されません。

<u> 前提条件 </u>:

* Adobe Commerce Inventory management（MSI）モジュールがインストールされている。
* バックオーダーは、「**[!UICONTROL Admin]**」 > 「**[!UICONTROL Store]**」 > 「**[!UICONTROL Configuration]**」 > 「**[!UICONTROL Catalog]**」 > 「**[!UICONTROL Inventory]**」 > 「**[!UICONTROL Product Stock Options]**」 > 「**[!UICONTROL Backorders]**」で有効化します。

<u> 再現手順 </u>:

1. 新しい在庫を作成します。
1. 新規ソースを作成します。
1. デフォルトの web サイトを新しい在庫に割り当て、新しいソースを割り当てます。
1. 新しい製品を作成します。

   * デフォルトのソース数量を 10 に、新しいソース数量を 0 に設定します。

1. 商品をストアフロントのカートに追加します。
1. チェックアウト時のバックオーダー警告を確認し、製品が新しいソースから来ていることを示します。
1. 注文します。
1. Admin で注文を開き、バックオーダーのステータスを確認します。

<u> 期待される結果 </u>:

この受注は、数量 1 がバックオーダーであることを示しています。

<u> 実際の結果 </u>:

この受注は、数量 1 がバックオーダーではなく受注済であることを示しています。

>[!MORELIKETHIS]
>
>[ 注文項目のステータスが正しく *[!UICONTROL Backordered]*](/help/support-tools/patches-available-in-qpt-tool/v1-1-33/acsd-51408-order-item-status-is-set-to-backordered.md)に設定されていません

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
