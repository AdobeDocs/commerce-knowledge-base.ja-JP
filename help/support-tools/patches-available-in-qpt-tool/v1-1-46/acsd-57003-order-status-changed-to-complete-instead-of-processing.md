---
title: 「ACSD-57003：注文のステータスが、*処理中*に変更されず、*完了*に変更される」
description: ACSD-57003 パッチを適用すると、注文のステータスが「処理中」ではなく「完了」に変わるAdobe Commerceの問題が修正されます。
feature: Orders, Invoices, Shipping/Delivery
role: Admin, Developer
exl-id: c3c59185-c447-46fa-b404-6c4a4a300315
source-git-commit: c5e94c6407394cd905ea470628d28db2c2c6c0ed
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# ACSD-57003：注文ステータスの変更先 *完了* ～に変わるのではなく *処理*

ACSD-57003 パッチは、注文ステータスが次のように変更される問題を修正します。 *完了* ～に変わるのではなく *処理*. このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.46 がインストールされています。 パッチ ID は ACSD-57003 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

注文のステータスが「」に変わります *完了* ～に変わるのではなく *処理* 注文が一部払い戻され、一部出荷された場合。

<u>再現手順</u>:

1. 2 つの設定可能な製品を使用して注文を作成します。
1. すべての品目の請求書を発行します。
1. 最初の品目のみを出荷します。
1. 出荷済品目のみの払戻/クレジット・メモの作成（*最初の項目*）に設定します。
1. 注文ステータスを確認します。

<u>期待される結果</u>:

注文ステータスは「」にする必要があります _処理_ 都道府県。

<u>実際の結果</u>:

注文ステータスが「」に変更されます *完了* 一部出荷済品目のクレジット・メモを作成した後。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
