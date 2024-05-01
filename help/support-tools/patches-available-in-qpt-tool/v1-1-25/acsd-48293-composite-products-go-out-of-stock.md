---
title: 「ACSD-48293：子供用製品の再入荷時に在庫切れになった複合製品」
description: ACSD-48293 パッチを適用すると、売り切れた子商品が在庫に戻ったときに複合商品が在庫切れになるAdobe Commerceの問題を修正できます。
exl-id: 74ca34fe-e015-4daf-a608-4756c8ab3558
feature: Admin Workspace, Orders, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# ACSD-48293：商品を再入荷した際、商品が売り切れた場合に商品が在庫切れになる複合製品

ACSD-48293 パッチは、売り切れた子製品が在庫に戻されたときに複合製品が在庫切れになる問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.25 がインストールされています。 パッチ ID は ACSD-48293 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

複合製品は、売り切れた子製品が在庫に戻されると、在庫切れになります。

<u>再現手順</u>:

1. セカンダリ web サイト、ストア、ストア表示を作成します。
1. 2 つのソースと在庫を作成し、各 web サイトに割り当てます。
1. の下の「在庫切れ製品を表示」オプションを有効にします **[!UICONTROL Store]** > **[!UICONTROL Config]** > **[!UICONTROL Catalog]** > **[!UICONTROL Inventory]** > **[!UICONTROL Stock Options]** > **[!UICONTROL Display Out-of-Stock Products]** = *[!UICONTROL Yes]*.
1. プライマリ web サイトの在庫ソースを使用して、1 つの関連製品と設定可能な製品を作成します（set qty = 1）。
1. 設定可能な商品を注文します。
1. cron を実行します。
1. ストアフロントから設定可能な製品を開き、在庫切れであることを確認します。
1. から設定可能な製品を開きます。 [!UICONTROL Admin] を設定して、 **[!UICONTROL Manage Stock Option]** 対象： *[!UICONTROL No]*.
1. cron を実行します。
1. 注文を発送し、在庫を作る簡単な製品に数量を追加します。
1. cron を実行します。
1. ストアフロントで商品の在庫状況を確認してください。

<u>期待される結果</u>:

設定可能な商品が在庫にあります。

<u>実際の結果</u>:

設定可能な商品の在庫がありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
