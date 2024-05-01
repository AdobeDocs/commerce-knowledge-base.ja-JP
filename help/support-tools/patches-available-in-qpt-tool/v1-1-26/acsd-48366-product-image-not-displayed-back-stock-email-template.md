---
title: '''ACSD-48366：製品画像がに表示されない [!UICONTROL Back to Stock] メールテンプレート'
description: ACSD-48366 パッチを適用すると、製品の在庫通知メールに製品のサムネール画像が表示されないAdobe Commerceの問題を修正できます。
exl-id: 57b549b0-6e97-4d5f-927e-9585f3257872
feature: Admin Workspace, Communications, Orders, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# ACSD-48366：製品画像がに表示されない [!UICONTROL Back to Stock] メールテンプレート

ACSD-48366 パッチは、製品の在庫通知メールに製品のサムネール画像が表示されない問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.26 がインストールされています。 パッチ ID は ACSD-48366 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

に製品画像が表示されません [!UICONTROL Back to Stock] メールテンプレート。

<u>再現手順</u>:

1. Enable （有効） *[!UICONTROL Product Alert]* （用） *[!UICONTROL Back in Stock]* ～に行くことによって **[!UICONTROL Store]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Product Alert]** > **[!UICONTROL Allow Alert When Product Comes Back in Stock]** = *[!UICONTROL Yes]*.
1. Enable （有効） *[!UICONTROL Display Out of Stock Products]* ～に行くことによって **[!UICONTROL Store]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Inventory]** > **[!UICONTROL Display Out of Stock]** = *[!UICONTROL Yes]*.
1. 数量= 0 の単純製品を作成します。
1. ストアフロントから顧客を作成し、上記の製品を購読して、在庫がある場合に製品アラートを取得します。
1. 商品を在庫にしてください。
1. 製品アラート cron を実行します。

   ```
   n98-magerun2.phar sys:cron:run catalog_product_alert
   ```

1. 顧客の製品アラートを開始します。

   ```
   bin/magento queue:consumers:start product_alert
   ```

1. メールを確認します。 在庫アラートメールがメールキャッチャーで使用できるようになりました。

<u>期待される結果</u>:

商品画像は、在庫アラートメールに表示されます。

<u>実際の結果</u>:

在庫通知メールに製品画像は表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
