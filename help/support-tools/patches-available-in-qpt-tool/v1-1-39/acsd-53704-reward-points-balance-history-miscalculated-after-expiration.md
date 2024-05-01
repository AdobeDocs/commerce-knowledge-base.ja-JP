---
title: 「ACSD-53704：報酬ポイントの残高履歴が有効期限後に正しく計算されない」
description: ACSD-53704 パッチを適用すると、報酬ポイントの有効期限が切れた後に報酬ポイントのバランス履歴が誤って計算されるAdobe Commerceの問題を修正できます。
feature: Rewards
role: Admin, Developer
exl-id: 5300cc22-0425-4467-b1e2-8bd799afb5fd
source-git-commit: dccb8dde1666fa0c72c7c94cd94c82daddaadc54
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# ACSD-53704：報酬ポイントのバランス履歴が有効期限後に計算されません

ACSD-53704 パッチは、報酬ポイントの有効期限が切れた後に報酬ポイントのバランス履歴が誤って計算される問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.39 がインストールされています。 パッチ ID は ACSD-53704 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

報酬ポイントの残高履歴は、報酬ポイントの有効期限後に誤って計算される。

<u>再現手順</u>:

1. ストアフロントで顧客を作成します。
1. 有効期限が異なる顧客の報酬ポイントを追加します。
1. を確認します `magento_reward_history` テーブルを作成して、報酬の最新レコードの有効期限を過去の日付に設定します：

   ```
   UPDATE magento_reward_history SET expired_at_static = '2023-08-24 10:47:38' WHERE history_id = 3;
   ```

1. の報酬履歴グリッドを確認します **[!UICONTROL Admin]** > **[!UICONTROL Customers]** > **[!UICONTROL All Customers]** > **[!UICONTROL Edit customer]** > **[!UICONTROL Reward points]** > **[!UICONTROL Reward Points History]** および **[!UICONTROL Reward Points Balance]**.

<u>期待される結果</u>:

報酬ポイントの残高には、有効期限が切れていないポイントのみが表示されます。

<u>実際の結果</u>:

報酬ポイントの残高には、有効期限切れのポイントが含まれる金額が反映されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
