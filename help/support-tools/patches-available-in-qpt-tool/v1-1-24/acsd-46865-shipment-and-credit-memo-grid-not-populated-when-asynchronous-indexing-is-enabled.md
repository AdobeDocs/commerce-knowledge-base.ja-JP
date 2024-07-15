---
title: 「ACSD-46865:[!UICONTROL asynchronous indexing] が有効な場合、[!UICONTROL shipment] と [!UICONTROL credit memo] が入力されない」
description: ACSD-46865 パッチを適用すると、[!UICONTROL asynchronous indexing] が有効になっているときに [!UICONTROL shipment] と [!UICONTROL credit memo] のグリッドが入力されないAdobe Commerceの問題を修正できます。
exl-id: 056177a8-42f0-4138-8c04-5b037d25dfd0
feature: Cache, Orders, Returns, Shipping/Delivery
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# ACSD-46865:[!UICONTROL asynchronous indexing] が有効な場合、[!UICONTROL shipment] と [!UICONTROL credit memo] が入力されない

ACSD-46865 パッチは、[!UICONTROL asynchronous indexing] が有効な場合に [!UICONTROL shipment] グリッドと [!UICONTROL credit memo] グリッドが入力されない問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.24 がインストールされている場合に使用できます。 パッチ ID は ACSD-46865 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.5-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

[!UICONTROL asynchronous indexing] が有効な場合、[!UICONTROL Shipment] および [!UICONTROL credit memo] グリッドは入力されません。

<u> 再現手順 </u>:

1. [!DNL Commerce] Admin で、**[!UICONTROL Set Stores]** / **[!UICONTROL Settings]** / **[!UICONTROL Configuration]** / **[!UICONTROL Advanced]** / **[!UICONTROL Developer]** / **[!UICONTROL Grid Settings]** / **[!UICONTROL Asynchronous indexing Enable]** = *YES* に移動します。
2. 再度、**[!UICONTROL Set Stores]**/**[!UICONTROL Settings]**/**[!UICONTROL Configuration]**/**[!UICONTROL Sales]**/**[!UICONTROL Sales]**/**[!UICONTROL Orders]**/**[!UICONTROL Invoices]**/**[!UICONTROL Shipments]**/**[!UICONTROL Credit Memos Archiving]**/**[!UICONTROL Enable Archiving]**=*[!UICONTROL YES]* に移動します。
3. 設定キャッシュをクリーンアップします。
4. シンプルな製品に対して新しいゲストを注文します。
5. cron を実行します。
6. **[!UICONTROL Sales]**/**[!UICONTROL Orders]** に移動して [!UICONTROL Commerce] Admin で注文を開き、請求書とクレジットメモを生成します。
7. 注文を [!UICONTROL Archive] に移動します。
8. シンプルな商品に対して別の注文を作成します。
9. cron を実行します。
10. 新規受注に移動し、新規出荷、請求書およびクレジット・メモを生成します。
11. cron を実行します。
12. 管理画面で [!UICONTROL shipments]、[!UICONTROL invoices]、[!UICONTROL credit memo] のグリッドを確認します。

<u> 期待される結果 </u>:

新しい [!UICONTROL shipment]、[!UICONTROL invoice] および [!UICONTROL credit memo] が表示されます。

<u> 実際の結果 </u>:

新しい [!UICONTROL shipment]、[!UICONTROL invoice]、[!UICONTROL credit memo] は表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
