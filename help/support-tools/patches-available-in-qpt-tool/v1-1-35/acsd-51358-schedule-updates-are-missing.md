---
title: 「ACSD-51358：スケジュールの更新がない」
description: ACSD-51358 パッチを適用すると、Adobe Commerceの問題を修正できます。この問題では、終了日を指定せずにスケジュールされた更新を変更すると、同じエンティティで他のスケジュールされた更新が削除されます。
feature: Staging
role: Admin, Developer
exl-id: 8bc4c505-9cf2-4c33-93a1-4b4d7d0dfc15
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# ACSD-51358: スケジュールの更新がありません

ACSD-51358 パッチでは、終了日を指定せずにスケジュールされた更新で変更を行うと、同じエンティティ上の他のスケジュールされた更新が削除される問題が修正されています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.35 がインストールされている場合に使用できます。 パッチ ID は ACSD-51358 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

終了日を指定せずにスケジュール済み更新を変更すると、同じエンティティ上の他のスケジュール済み更新が削除されます。

<u> 再現手順 </u>:

1. 終了日のない **[!UICONTROL scheduled update]** を作成します（*更新 1*）。
1. 最初の更新と同じ開始日で、次の日と終了日（*更新 2*）を追加する新しい **[!UICONTROL scheduled update]** を作成します。
1. 手順 1 （*更新 1*）で作成した **[!UICONTROL scheduled update]** を編集して、変更を保存します。

<u> 期待される結果 </u>

（*update 1*）を編集した場合、（*update 2*）は **[!UICONTROL schedule update]** のリストに残ります。

<u> 実績 </u>

（*update 2*）は、（*update 1*）が編集されたときに、**[!UICONTROL schedule update]** のリストから削除されました。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html>) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>)」を参照してください。
