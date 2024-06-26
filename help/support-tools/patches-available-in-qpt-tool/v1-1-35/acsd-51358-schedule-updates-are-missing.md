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

ACSD-51358 パッチでは、終了日を指定せずにスケジュールされた更新で変更を行うと、同じエンティティ上の他のスケジュールされた更新が削除される問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.35 がインストールされています。 パッチ ID は ACSD-51358 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

終了日を指定せずにスケジュール済み更新を変更すると、同じエンティティ上の他のスケジュール済み更新が削除されます。

<u>再現手順</u>:

1. を作成 **[!UICONTROL scheduled update]** 終了日（*更新 1*）に設定します。
1. 新規作成 **[!UICONTROL scheduled update]** 開始日が最初の更新と同じ、ただし翌日と終了日を追加する（*更新 2*）に設定します。
1. 編集 **[!UICONTROL scheduled update]** 手順 1 で作成（*更新 1*）を選択して、変更内容を保存します。

<u>期待される結果</u>

この（*更新 2*）は、に残す必要があります。 **[!UICONTROL schedule update]** リスト条件（*更新 1*）が編集されました。

<u>実際の結果</u>

この（*更新 2*）がから削除されました **[!UICONTROL schedule update]** リスト条件（*更新 1*）が編集されました。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
