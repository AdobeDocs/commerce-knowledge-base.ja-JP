---
title: 「ACSD-52287：アーカイブした注文のステータスが変更されない」
description: ACSD-52287 パッチを適用すると、クレジットメモが送信された後、アーカイブされた注文のステータスがグリッド上で*完了*から*クローズ*に変わらないAdobe Commerceの問題を修正できます。
feature: Orders, Checkout
role: Admin, Developer
exl-id: c88c5c87-eec7-4105-9e4e-815d0888a34b
source-git-commit: 178023177975f210ebf7dd07e8c75cfe3ac89ff1
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# ACSD-52287: アーカイブ済オーダーのステータスは変更されない

ACSD-52287 パッチは、アーカイブされた注文のステータスがから変更されない問題を修正します *完了* 対象： *クローズ* クレジット・メモが発行された後のグリッド。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.38 がインストールされています。 パッチ ID は ACSD-52287 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

アーカイブ済オーダーのステータスが次のように変更されることはありません。 *完了* 対象： *クローズ* クレジット・メモが発行された後のグリッド。

<u>再現手順</u>:

1. 設定 *[!UICONTROL Asynchronous Indexing]*.
   * 管理サイドバーで、に移動します。 **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]**.
   * 左側のパネルで、を展開します **[!UICONTROL Advanced]** セクションで選択 **[!UICONTROL Developer]** その下に。
   * を展開します。 **[!UICONTROL Grid Settings]** セクション。
   * を設定 *[!UICONTROL Asynchronous indexing]* 対象： *はい*.
   * クリック **[!UICONTROL Save Config]**.
1. の設定 *[!UICONTROL Order Archive]*.
   * 管理サイドバーで、に移動します。 **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]**.
   * 左側のパネルで、を展開します **[!UICONTROL Sales]** セクションで選択 **[!UICONTROL Sales]** その下に。
   * を展開します。 **[!UICONTROL Orders, Invoices, Shipments, Credit Memos Archiving]** セクション。
   * を設定 *[!UICONTROL Enable Archiving]* 対象： *はい* （残りの設定はデフォルトのままにします）。
   * クリック **[!UICONTROL Save Config]**.
1. フロントエンドに注文します。
1. を実行 [!DNL cron]  ～に現れるために *[!UICONTROL Admin Order Grid]*.
1. 注文ステータスを更新する注文を請求および出荷 *完了*.
1. を実行 [!DNL cron]  を更新します *[!UICONTROL Sales Order Grid]* 最新の注文ステータスが表示されます。
1. 注文をアーカイブします。
1. に移動します *[!UICONTROL Archived order grid]*.
1. アーカイブした注文を開き、オフラインで以下を作成して返金します。 [!UICONTROL Credit Memo] を作成するには [!UICONTROL Order status]: *クローズ*.
1. を実行 [!DNL cron] 数回。
1. を確認します *[!UICONTROL Archived order grid]* 新しい注文ステータス

<u>期待される結果</u>:

順序は次のように表示されます *クローズ*.

<u>実際の結果</u>:

順序は次のように表示されます *完了*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
