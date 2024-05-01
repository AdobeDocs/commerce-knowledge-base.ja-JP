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

ACSD-48773 パッチは、報酬ポイントのメールテンプレートが間違ったストアから取得される問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.26 がインストールされています。 パッチ ID は ACSD-48773 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

バンドル製品がどの web サイトにも割り当てられていない場合、製品の価格の再インデックスが機能しません。

<u>再現手順</u>:

1. 2 つの web サイト、2 つのストア、2 つのストアビューを作成します。
1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Product Reviews]** および有効化 **[!UICONTROL Reviews]**.
1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Store Email Addresses]**.
に切り替え **[!DNL default website scope]**、を設定します。 **[!UICONTROL Customer Support Sender Email]** 住所（例： *support_base@example.com*）に設定します。
に切り替え **[!DNL second website scope]**、を設定します。 **[!UICONTROL Customer Support Sender Email]** アドレスを別の値に変更（例： *support_second@example.com*）に設定します。
1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Customers]** > **[!UICONTROL Customer Configuration]** > **[!UICONTROL Account Sharing Options]** > **[!UICONTROL Share Customer Accounts]**、およびを設定 **[!UICONTROL Share Customer Accounts]** = *Web サイトあたり*.
1. 次の下 **[!UICONTROL Reward Points]**、次の設定をおこないます。
   **[!UICONTROL Enable Reward Points Functionality]** = *はい*
   **[!UICONTROL Enable Reward Points Functionality on Storefront]** = *はい*
   **[!UICONTROL Actions for Acquiring Reward Points by Customers]** > **[!UICONTROL Review Submission]** およびを設定 **[!UICONTROL Review Submission]** = *150*
   **[!UICONTROL Email Notification Settings]** > **[!UICONTROL Email Sender]** およびを設定 **[!UICONTROL Email Sender]** = *カスタマーサポート*
1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Other Settings]** > **[!UICONTROL Reward Exchange Rates]** 2 つ目の web サイトの為替レートを設定します **[!UICONTROL Points/Currency]** および **[!UICONTROL Currency/Points]**.
1. 2 番目の web サイトに顧客アカウントを作成します。
1. 2 番目の Web サイトで、顧客としてログインします。
1. 必ずを有効にします。 **[!UICONTROL Subscribe]** （用） **[!UICONTROL Balance Updates]**.
1. 製品レビューを送信します。
1. に移動 **[!UICONTROL Marketing]** > **[!UICONTROL User Content]** > **[!UICONTROL Pending Reviews]**.
1. 新しいレビューのステータスをに変更します。 ***[!UICONTROL Approved]*** および **[!UICONTROL Save]**.
1. メールが届くのを待ちます。

<u>期待される結果</u>:

報酬ポイントの更新メールは、2 番目の web サイト範囲に設定されたメール送信者が送信する必要があります。

<u>実際の結果</u>:

報酬ポイントの更新メールは、デフォルトの web サイト範囲に設定されたメール送信者から送信されました。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
