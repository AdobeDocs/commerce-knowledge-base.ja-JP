---
title: 「ACSD-48910：複数のソースが割り当てられたバンドル製品が、請求書と発送後に在庫切れになる」
description: ACSD-48910 パッチを適用すると、複数のソースに割り当てられたバンドル製品が、注文の請求および出荷後に（まだ数量がゼロ以外の場合でも）在庫切れになるAdobe Commerceの問題を修正できます。
feature: Products, Inventory
role: Admin, Developer
exl-id: 6ac3dedf-1c28-4874-b963-44a429b37983
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# ACSD-48910：複数のソースが割り当てられたバンドル製品が、請求書および発送後に在庫切れになる

ACSD-48910 パッチは、複数のソースに割り当てられたバンドル製品が注文の請求および出荷後に在庫切れになる問題を修正します（数量がまだ 0 以外の場合でも）。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.42 がインストールされています。 パッチ ID は ACSD-48910 です。 この問題はAdobe Commerce 2.4.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.5-p5

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

複数のソースに割り当てられたバンドル製品は、まだ使用可能な場合でも、請求および出荷後に在庫切れになります。

<u>再現手順</u>:

1. 2 つの web サイトを作成します。
1. 2 つのストア/ストアビューを作成します（Web サイトごとに 1 つ）。
1. 2 つのシンプルな製品（数量= 10）を作成し、それらを在庫と web サイトの両方に割り当てます。
1. バンドルされた製品を作成し、これらのシンプルな製品をそれに追加します。 バンドルされた製品を両方の web サイトに割り当てます。
1. ストアフロントに移動し、バンドルされた製品を買い物かごに追加します。
1. チェックアウトして注文します。
1. 管理者から、注文を請求して出荷します。

<u>期待される結果</u>:

10 個の商品のうち 1 個しか購入していないため、バンドルされた商品は在庫として残っています。

<u>実際の結果</u>:

バンドルされた製品のステータスが在庫切れに変更されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
