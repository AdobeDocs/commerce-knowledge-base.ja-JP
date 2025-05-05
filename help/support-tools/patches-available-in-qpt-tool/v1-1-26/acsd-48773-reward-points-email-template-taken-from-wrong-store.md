---
title: 「ACSD-48773：報酬ポイントのメールテンプレートが間違ったストアから取得される」
description: ACSD-48773 パッチを適用して、報酬ポイントのメールテンプレートが間違ったストアから取得されるAdobe Commerceの問題を修正してください。
exl-id: 96dda97c-5177-4883-ad2b-709928cb5f4d
feature: Admin Workspace, Communications, Marketing Tools, Orders, Personalization, Rewards
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# ACSD-48773：報酬ポイントのメールテンプレートが間違ったストアから取得される

ACSD-48773 パッチは、報酬ポイントのメールテンプレートが間違ったストアから取得される問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.26 がインストールされている場合に使用できます。 パッチ ID は ACSD-48773 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

バンドル製品がどの web サイトにも割り当てられていない場合、製品の価格の再インデックスが機能しません。

<u> 再現手順 </u>:

1. 2 つの web サイト、2 つのストア、2 つのストアビューを作成します。
1. **[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Catalog]**/**[!UICONTROL Product Reviews]** に移動し、**[!UICONTROL Reviews]** を有効にします。
1. **[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Store Email Addresses]** に移動します。
**[!DNL default website scope]** に切り替え、**[!UICONTROL Customer Support Sender Email]** アドレスを設定します（例：*support_base@example.com*）。
**[!DNL second website scope]** に切り替え、**[!UICONTROL Customer Support Sender Email]** アドレスを別の値に設定します（例：*support_second@example.com*）。
1. **[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Customers]**/**[!UICONTROL Customer Configuration]**/**[!UICONTROL Account Sharing Options]**/**[!UICONTROL Share Customer Accounts]** に移動し、**[!UICONTROL Share Customer Accounts]**=*Web サイトごと* に設定します。
1. 「**[!UICONTROL Reward Points]**」で、次の設定を行います。
   **[!UICONTROL Enable Reward Points Functionality]** = *はい*
   **[!UICONTROL Enable Reward Points Functionality on Storefront]** = *はい*
   **[!UICONTROL Actions for Acquiring Reward Points by Customers]** > **[!UICONTROL Review Submission]**、set **[!UICONTROL Review Submission]** = *150*
   **[!UICONTROL Email Notification Settings]**/**[!UICONTROL Email Sender]** を選択し、**[!UICONTROL Email Sender]** を設定= *カスタマーサポート*
1. **[!UICONTROL Stores]**/**[!UICONTROL Other Settings]**/**[!UICONTROL Reward Exchange Rates]** に移動し、**[!UICONTROL Points/Currency]** と **[!UICONTROL Currency/Points]** の両方の 2 番目の web サイトの為替レートを設定します。
1. 2 番目の web サイトに顧客アカウントを作成します。
1. 2 番目の Web サイトで、顧客としてログインします。
1. **[!UICONTROL Balance Updates]** で **[!UICONTROL Subscribe]** を必ず有効にしてください。
1. 製品レビューを送信します。
1. **[!UICONTROL Marketing]**/**[!UICONTROL User Content]**/**[!UICONTROL Pending Reviews]** に移動します。
1. 新しいレビューのステータスを ***[!UICONTROL Approved]*** と **[!UICONTROL Save]** に変更します。
1. メールが届くのを待ちます。

<u> 期待される結果 </u>:

報酬ポイントの更新メールは、2 番目の web サイト範囲に設定されたメール送信者が送信する必要があります。

<u> 実際の結果 </u>:

報酬ポイントの更新メールは、デフォルトの web サイト範囲に設定されたメール送信者から送信されました。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
