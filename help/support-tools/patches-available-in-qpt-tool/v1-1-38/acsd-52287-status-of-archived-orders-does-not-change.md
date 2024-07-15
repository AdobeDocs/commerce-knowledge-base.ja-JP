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

ACSD-52287 パッチは、クレジット・メモが送信された後、アーカイブ済の注文のステータスがグリッド上で *完了* から *クローズ* に変更されない問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.38 がインストールされている場合に使用できます。 パッチ ID は ACSD-52287 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6-p2

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

クレジット・メモが発行された後、アーカイブ済受注のステータスがグリッド上で *完了* から *クローズ* に変更されることはありません。

<u> 再現手順 </u>:

1. *[!UICONTROL Asynchronous Indexing]* の設定
   * 管理者サイドバーで、**[!UICONTROL Stores]**/**[!UICONTROL Settings]**/**[!UICONTROL Configuration]** に移動します。
   * 左側のパネルで「**[!UICONTROL Advanced]**」セクションを展開し、その下 **[!UICONTROL Developer]** 選択します。
   * 「**[!UICONTROL Grid Settings]**」セクションを展開します。
   * *[!UICONTROL Asynchronous indexing]* を *はい* に設定します。
   * 「**[!UICONTROL Save Config]**」をクリックします。
1. *[!UICONTROL Order Archive]* を設定します。
   * 管理者サイドバーで、**[!UICONTROL Stores]**/**[!UICONTROL Settings]**/**[!UICONTROL Configuration]** に移動します。
   * 左側のパネルで「**[!UICONTROL Sales]**」セクションを展開し、その下 **[!UICONTROL Sales]** 選択します。
   * 「**[!UICONTROL Orders, Invoices, Shipments, Credit Memos Archiving]**」セクションを展開します。
   * *[!UICONTROL Enable Archiving]* を *はい* に設定します（残りの設定はデフォルトのままにします）。
   * 「**[!UICONTROL Save Config]**」をクリックします。
1. フロントエンドに注文します。
1. *[!UICONTROL Admin Order Grid]* に表示するには、[!DNL cron] を実行します。
1. 注文のステータスを *完了* に更新するには、注文を請求および出荷します。
1. [!DNL cron] を実行して、*[!UICONTROL Sales Order Grid]* を最新の注文ステータスで更新します。
1. 注文をアーカイブします。
1. *[!UICONTROL Archived order grid]* に行きなさい。
1. [!UICONTROL Credit Memo] アーカイブされた注文を開き、[!UICONTROL Order status] を作成してオフラインで注文を返金します。*Closed*。
1. [!DNL cron] を数回実行します。
1. 新しい注文ステータスの *[!UICONTROL Archived order grid]* を確認します。

<u> 期待される結果 </u>:

注文が *クローズ* と表示されます。

<u> 実際の結果 </u>:

注文が *完了* と表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
