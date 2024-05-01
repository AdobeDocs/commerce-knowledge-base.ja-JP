---
title: 'ACSD-46865: [!UICONTROL shipment] および [!UICONTROL credit memo] 次の場合は生成されません： [!UICONTROL asynchronous indexing] 有効'
description: Adobe Commerceの問題を修正するために ACSD-46865 パッチを適用してください。この問題の場所は次のとおりです。 [!UICONTROL shipment] および [!UICONTROL credit memo] 次の場合、グリッドは入力されません [!UICONTROL asynchronous indexing] が有効になっています。
exl-id: 056177a8-42f0-4138-8c04-5b037d25dfd0
feature: Cache, Orders, Returns, Shipping/Delivery
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# ACSD-46865: [!UICONTROL shipment] および [!UICONTROL credit memo] 次の場合は生成されません： [!UICONTROL asynchronous indexing] 有効

ACSD-46865 パッチは、次の問題を修正します。 [!UICONTROL shipment] および [!UICONTROL credit memo] 次の場合、グリッドは入力されません [!UICONTROL asynchronous indexing] が有効になっています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.24 がインストールされています。 パッチ ID は ACSD-46865 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

[!UICONTROL Shipment] および [!UICONTROL credit memo] 次の場合、グリッドは入力されません [!UICONTROL asynchronous indexing] が有効になっています。

<u>再現手順</u>:

1. が含まれる [!DNL Commerce] 管理者、に移動します **[!UICONTROL Set Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL Developer]** > **[!UICONTROL Grid Settings]** > **[!UICONTROL Asynchronous indexing Enable]** = *はい*.
2. 再び以下に移動 **[!UICONTROL Set Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** > **[!UICONTROL Sales]** > **[!UICONTROL Orders]** > **[!UICONTROL Invoices]** > **[!UICONTROL Shipments]** > **[!UICONTROL Credit Memos Archiving]** > **[!UICONTROL Enable Archiving]** = *[!UICONTROL YES]*.
3. 設定キャッシュをクリーンアップします。
4. シンプルな製品に対して新しいゲストを注文します。
5. cron を実行します。
6. で注文を開きます [!UICONTROL Commerce] に移動して管理します **[!UICONTROL Sales]** > **[!UICONTROL Orders]** 請求書およびクレジット・メモを生成します。
7. オーダーを移動 [!UICONTROL Archive].
8. シンプルな商品に対して別の注文を作成します。
9. cron を実行します。
10. 新規受注に移動し、新規出荷、請求書およびクレジット・メモを生成します。
11. cron を実行します。
12. を確認します [!UICONTROL shipments], [!UICONTROL invoices]、および [!UICONTROL credit memo] 管理画面のグリッド。

<u>期待される結果</u>:

新規 [!UICONTROL shipment], [!UICONTROL invoice] および [!UICONTROL credit memo] が表示されます。

<u>実際の結果</u>:

新規 [!UICONTROL shipment], [!UICONTROL invoice]、および [!UICONTROL credit memo] が表示されない。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
