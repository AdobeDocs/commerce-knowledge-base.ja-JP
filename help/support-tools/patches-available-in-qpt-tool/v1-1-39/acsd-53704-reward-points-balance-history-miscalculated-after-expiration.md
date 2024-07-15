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

ACSD-53704 パッチは、報酬ポイントの有効期限が切れた後に報酬ポイントのバランス履歴が誤って計算される問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.39 がインストールされている場合に使用できます。 パッチ ID は ACSD-53704 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

報酬ポイントの残高履歴は、報酬ポイントの有効期限後に誤って計算される。

<u> 再現手順 </u>:

1. ストアフロントで顧客を作成します。
1. 有効期限が異なる顧客の報酬ポイントを追加します。
1. `magento_reward_history` テーブルを確認し、報酬ポイントの最新レコードの有効期限を過去の日付に設定します。

   ```
   UPDATE magento_reward_history SET expired_at_static = '2023-08-24 10:47:38' WHERE history_id = 3;
   ```

1. **[!UICONTROL Admin]**/**[!UICONTROL Customers]**/**[!UICONTROL All Customers]**/**[!UICONTROL Edit customer]**/**[!UICONTROL Reward points]**/**[!UICONTROL Reward Points History]** および **[!UICONTROL Reward Points Balance]** の報酬履歴グリッドを確認します。

<u> 期待される結果 </u>:

報酬ポイントの残高には、有効期限が切れていないポイントのみが表示されます。

<u> 実際の結果 </u>:

報酬ポイントの残高には、有効期限切れのポイントが含まれる金額が反映されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
