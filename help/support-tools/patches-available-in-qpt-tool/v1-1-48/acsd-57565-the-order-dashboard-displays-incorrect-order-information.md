---
title: 「ACSD-57565：注文ダッシュボードに間違った注文情報が表示される」
description: ACSD-57565 パッチを適用すると、期間が更新されるまで注文ダッシュボードに誤った注文情報が表示されるAdobe Commerceの問題を修正できます。
feature: Roles/Permissions
role: Admin, Developer
exl-id: 5b292fef-23f6-479f-bf76-adad53d30cf4
source-git-commit: fdf6e6e85f903a26a7b44674937ccf88ee769d06
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# ACSD-57565：注文ダッシュボードに間違った注文情報が表示される

ACSD-57565 パッチは、期間が更新されるまで注文ダッシュボードに間違った注文情報が表示される問題を修正します。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.48 がインストールされています。 パッチ ID は ACSD-57565 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます

## 問題

注文ダッシュボードに間違った注文情報が表示される。

<u>再現手順</u>:

1. Enable （有効） **[!UICONTROL dashboard charts]**.
1. オーダーを作成して請求します。
1. 注文作成時から少なくとも 24 時間待ちます。
1. を確認します **[!UICONTROL dashboard chart]** データ。
1. 注文総数をメモします。
1. 時間をに変更します *今月*&#x200B;に変更してから、に戻します *今日*.

<u>期待される結果</u>:

ダッシュボードグラフには、常に正しい統計が表示されます。

<u>実際の結果</u>:

ダッシュボードグラフは、最初の読み込み時に間違った統計を表示します。 グラフの正確な統計は、期間の終了後に更新されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
