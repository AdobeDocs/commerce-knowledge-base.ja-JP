---
title: 「ACSD-52202：デフォルト以外の在庫が注文で 0 数量に設定されると、デフォルトの在庫販売可能数量がエラーで 0 に変更される」
description: 注文でデフォルト以外の在庫が数量 0 に設定されている場合に、デフォルトの在庫販売可能数量が誤って 0 に変わるAdobe Commerceの問題を修正するために、ACSD-52202 パッチを適用します。
feature: Inventory, Products
role: Admin
exl-id: 8a3b5da4-cf16-41c8-b2d5-b740d638c745
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# ACSD-52202：注文でデフォルト以外の在庫が数量 0 に設定されると、デフォルトの在庫販売可能数量がエラーで 0 に変更される

ACSD-52202 パッチは、注文でデフォルト以外の在庫が 0 数量に設定されている場合に、デフォルトの在庫販売可能数量（数量）がエラーで 0 に変更される問題を修正します。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.35 がインストールされています。 パッチ ID は ACSD-52202 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

注文でデフォルト以外の在庫が 0 数量に設定されている場合、デフォルトの在庫販売可能数量がエラーで 0 に変更される。

<u>再現手順</u>:

1. にログインします [!DNL Admin].
1. 作成 **website2**.
1. カスタムを作成 **ソース 2**.
1. カスタムを作成 **stock2**.
1. を割り当てる **ソース 2** および **stock2** 対象： **website1** さらに、デフォルトのソースとデフォルトの web サイトへの在庫を指定します。
1. シンプルな製品を作成して割り当て **数量** = *10* デフォルトのソースおよびの場合 **数量** = *1* の場合 **ソース 2** ソース。
1. 注文する **数量** = *1* （用） **website2**.
1. 請求書と出荷を作成します。
1. シンプルな製品を確認する **売れる量**.

<u>期待される結果</u>:

この **売れる量** = *10* （用） **ソース 2**.

<u>実際の結果</u>:

この **売れる量** = *0* 両方のソース用。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
