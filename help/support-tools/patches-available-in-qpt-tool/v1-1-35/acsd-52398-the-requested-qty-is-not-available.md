---
title: 「ACSD-52398：バンドルされた製品の数量を更新しようとすると、リクエストされた数量が使用できない」
description: ACSD-52398 パッチを適用すると、ストアフロントでカートにバンドルされた商品の数量を更新しようとすると、要求された数量が使用できないAdobe Commerceの問題を修正できます。
feature: Shopping Cart, Quotes, Products
role: Admin
exl-id: 7b7f06ac-7913-4603-992a-a5620045d828
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# ACSD-52398: バンドルされた製品の数量を更新しようとすると、要求数量を使用できません

ACSD-52398 パッチでは、ストアフロントでカートにバンドルされた製品の数量を更新しようとすると、要求された数量が使用できない問題が修正されています。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.35 がインストールされています。 パッチ ID は ACSD-52398 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ストアフロントでカート内のバンドル製品の数量を更新しようとすると、リクエストされた数量は使用できません。

<u>再現手順</u>:

1. 数量を含む 2 つのシンプルな製品の作成 *1* および *10*.
1. シンプルな製品を使用して、バンドルされた製品を作成します。
1. バンドルされた製品を買い物かごに追加します。
1. 製品を編集し、数量をに更新しようとします *3* オプションの場合、 *10* 個の項目が使用可能です。

<u>期待される結果</u>:

エラーはありません。 数量は次の理由により正常に更新されました *10* このオプションの在庫品目。

<u>実際の結果</u>:

次のエラーが発生します。 *リクエストされた数量は使用できません*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
