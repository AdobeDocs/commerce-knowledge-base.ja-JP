---
title: 'ACSD-51431: インデクサーのステータスは*[!UICONTROL Working]* changelog にエントリがないにもかかわらず'
description: ACSD-51431 パッチを適用して、インデクサーのステータスが*であるAdobe Commerceの問題を修正します。[!UICONTROL Working]*変更ログにエントリがない場合でも。
feature: Logs, Price Indexer
role: Admin
exl-id: 85977b78-7f6b-47c7-b33e-16668bdf98fe
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# ACSD-51431: インデクサーのステータスが *[!UICONTROL Working]* 変更ログにエントリがない場合でも

ACSD-51431 パッチは、インデクサーのステータスがであるパフォーマンスの問題を修正します *[!UICONTROL Working]* 変更ログにエントリがない場合でも。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.33 がインストールされています。 パッチ ID は ACSD-51431 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 - 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

インデクサーのステータスは *[!UICONTROL Working]* 変更ログにエントリがない場合でも。

<u>再現手順</u>:

1. を設定 **[!UICONTROL indexers]** 対象： [!UICONTROL Update on Schedule].
1. cron ジョブを毎分実行するように設定します。
1. 異なる製品への変更を同時に保存します。
1. 実行 `bin/magento indexer:status` 数分で完了します。

<u>期待される結果</u>:

変更内容が処理され、インデクサーがに置かれます *[!UICONTROL Ready]* ステータス。 この *[!UICONTROL Schedule]* ステータス : *[!UICONTROL idle (0 in the backlog)]*.

<u>実際の結果</u>:

変更内容が処理され、インデクサーがに置かれます *[!UICONTROL Ready]* ステータス。 ただし、 *[!UICONTROL Schedule]* ステータス表示 *[!UICONTROL working (0 in the backlog)]*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
