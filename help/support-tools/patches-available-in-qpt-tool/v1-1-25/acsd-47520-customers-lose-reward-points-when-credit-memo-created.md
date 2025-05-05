---
title: 「ACSD-47520：クレジットメモを作成すると顧客が報酬ポイントを失う」
description: ACSD-47520 パッチを適用すると、クレジットメモの作成時に顧客が報酬ポイントを失うAdobe Commerceの問題を修正できます。
exl-id: 748b4e05-981d-49f6-a4f5-b121d57085f4
feature: Admin Workspace, Cache, Orders, Rewards, Returns
role: Admin
source-git-commit: 3eeb86c2644f8a04ddcf5e205bc400d2ca9969af
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# ACSD-47520：クレジットメモを作成すると、顧客が報酬ポイントを失う

ACSD-47520 パッチは、クレジットメモが作成されたときに顧客が報酬ポイントを失う問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.25 がインストールされている場合に使用できます。 パッチ ID は ACSD-47520 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5-p4

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

クレジット メモを作成すると、顧客は報酬ポイントを失います。

<u> 再現手順 </u>:

1. Adobe Commerce管理者/ **[!UICONTROL Store]** / **[!UICONTROL Settings]** / **[!UICONTROL Configuration]** / **[!UICONTROL Customers]** / **[!UICONTROL Reward Points]** に移動します。
1. 設定を変更します。
   * **[!UICONTROL Enable Reward Points Functionality]** = _はい_
   * **[!UICONTROL Enable Reward Points Functionality on Storefront]** = _はい_
   * **[!UICONTROL Customers May See Reward Points History]** = _はい_
   * **[!UICONTROL Refund Reward Points Automatically]** = _いいえ_
   * **[!UICONTROL Deduct Reward Points from Refund Amount Automatically]** = _はい_
1. 管理者/ **[!UICONTROL Store]** / **[!UICONTROL Other Settings]** / **[!UICONTROL Reward Exchange Rates]** に移動し、「**[!UICONTROL Add New Rate]**」をクリックします。
1. 新しいレート（1:1）を追加し、キャッシュをフラッシュします。
1. 顧客を作成し、このアカウントに 10 の報酬ポイントを追加します。
1. 管理者/ **[!UICONTROL Sales]** / **[!UICONTROL Orders]** / **[!UICONTROL Create New Order]** /に移動し、前の手順で作成した顧客を選択します。
1. 価格が報酬ポイントよりも大きい製品を選択します。
1. 任意の支払い方法と報酬ポイントを介して注文を行います。
1. 注文の請求書を作成します。
1. クレジットメモを作成しますが、報酬ポイントは払い戻しません。

<u> 期待される結果 </u>:

* 管理者は報酬ポイントを返金できます。

* 注文ステータスがクローズされます。

<u> 実際の結果 </u>:

* 報酬ポイントを払い戻す方法はありません。

* 注文ステータスは「**[!UICONTROL Completed]**」です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
