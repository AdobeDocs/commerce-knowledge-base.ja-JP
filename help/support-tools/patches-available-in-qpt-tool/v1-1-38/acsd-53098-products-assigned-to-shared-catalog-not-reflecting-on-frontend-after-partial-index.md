---
title: 「ACSD-53098：共有カタログ内の製品がフロントエンドに反映されない」
description: ACSD-53098 パッチを適用すると、共有カタログに割り当てられた商品が部分的なインデックスを実行したときにフロントエンドに反映されないAdobe Commerceの問題を修正できます。
feature: B2B, Catalog Management, Categories, Products
role: Admin, Developer
exl-id: 19c66a3a-04b2-48ee-aff3-ad2b592ff876
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# ACSD-53098：共有カタログ内の製品がフロントエンドに反映されない

ACSD-53098 パッチは、共有カタログに割り当てられた製品が部分的なインデックスを実行したときにフロントエンドに反映されない問題を修正します。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.38 がインストールされています。 パッチ ID は ACSD-53098 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 - 2.4.3-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

API を介して共有カタログに割り当てられた製品は、部分インデクサーが cron ジョブを実行し、その後に消費者 cron が実行された後は、フロントエンドに表示されません。

<u>再現手順</u>:

1. の設定 [!DNL RabbitMQ] キューサービスとして使用します。
1. インデクサーをに切り替え **[!UICONTROL Update on Schedule]** モード。
1. 共有カタログを作成して会社に割り当てます。
1. シンプルな製品を作成してカテゴリに割り当てます。 部分再インデックスを実行します。

   `bin/magento cron:run --group=index --bootstrap=standaloneProcessStarted=1`

1. 次の API リクエストを使用して、作成した製品を共有カタログに割り当てます。

   ```
   pub/rest/all/V1/sharedCatalog/<id>/assignProducts
   {
       "products":[{
           "sku": "24-MB06"
           }
       ]
   }
   ```

1. 次の cron を実行してキューをクリアし、部分再インデックスを実行します。

   `bin/magento cron:run --group=consumers`

   `bin/magento cron:run --group=index --bootstrap=standaloneProcessStarted=1`

1. 会社のユーザーとしてフロントエンドにログインします。
1. フロントエンドカテゴリページを確認します。

<u>期待される結果</u>:

新しく割り当てられた製品がフロントエンドに表示されます。

<u>実際の結果</u>:

新しく割り当てられた製品は、フロントエンドには表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
