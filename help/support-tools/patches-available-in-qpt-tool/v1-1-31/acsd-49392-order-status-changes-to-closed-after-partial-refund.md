---
title: 「ACSD-49392：注文ステータスが、一部払い戻しの後にクローズに変更される」
description: ACSD-49392 パッチを適用すると、バンドルされた製品の部分払い戻し後に注文ステータスがクローズに変わるAdobe Commerceの問題を修正できます。
exl-id: fca6f502-e224-4444-b0d0-f823853c9458
feature: Orders
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# ACSD-49392：一部払い戻し後に注文ステータスがクローズに変更される

ACSD-49392 パッチは、バンドルされた製品の部分払い戻し後に注文ステータスがクローズに変更される問題を修正します。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.31 がインストールされています。 パッチ ID は ACSD-49392 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.3.7-p4 および 2.4.1 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

バンドルされた製品の一部払い戻し後、注文ステータスが「クローズ」に変更される。

<u>再現手順</u>:

1. Adobe Commerceにログインしてバンドル製品を作成するか、既存のバンドル製品を使用します。
1. このバンドル製品を 1 より多い数量で注文します。
1. 管理者に移動し、手順 2 で作成した注文を開きます。 **[!UICONTROL Sales]** > **[!UICONTROL Order]** 請求書を作成します。 注文ステータスを確認します。 処理中です。
1. 一部のクレジットメモを作成します（バンドル内のすべての製品に対して払い戻しを行わないでください）。
1. 注文ステータスを確認します。

<u>期待される結果</u>

バンドルされた製品の一部のクレジットメモを作成した後、注文ステータスは「処理中」になります。

<u>実際の結果</u>

バンドル製品の一部のクレジット・メモを作成すると、受注ステータスは「完了」になります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
