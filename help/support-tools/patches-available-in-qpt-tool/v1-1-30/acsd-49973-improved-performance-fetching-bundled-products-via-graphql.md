---
title: 'ACSD-49973：を介したバンドル製品の取得でパフォーマンスが向上しました [!DNL GraphQL]'
description: を介してバンドルされた製品を取得する際にパフォーマンスが低下するAdobe Commerceの問題を修正するために、ACSD-49973 パッチを適用してください。 [!DNL GraphQL].
exl-id: 7d7fce0f-40f9-4dec-aee7-1014690ccd7c
feature: GraphQL, Products
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# ACSD-49973：を介したバンドル製品の取得パフォーマンスの向上 [!DNL GraphQL]

ACSD-49973 パッチは、バンドルされた製品の次の場所からの取得パフォーマンスを向上させます。 [!DNL GraphQL]. このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.30 がインストールされています。 パッチ ID は ACSD-49973 です。 この問題はAdobe Commerce 2.4.7 で修正されていることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.4-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

を介してバンドルされた製品を取得すると、パフォーマンスが低下します。 [!DNL GraphQL].

<u>前提条件</u>:

を使用して 2000 バンドル製品を作成 [パフォーマンスツールキット](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/generate-data.html).

<u>再現手順</u>:

1. を有効にする [!DNL DB] クエリロガー：

   ```
   bin/magento dev:query-log:enable
   ```

1. 次を実行します [!DNL GraphQL] クエリ :

   ```GraphQL
   {
     products(
       search: "bundle"
       pageSize: 2000,
       sort: { relevance: DESC }
     ) {
       total_count
       items {
         name
         sku
       }
     }
   }
   ```

1. チェック `var/log/db.log` に対するリクエスト `catalog_product_bundle_selection` テーブル。

<u>期待される結果</u>:

に対するリクエスト `catalog_product_bundle_selection` テーブルはに存在しません `var/log/db.log`.

<u>実際の結果</u>:

に対するリクエストは 2000 件あります `catalog_product_bundle_selection` 同時にトリガーされ、パフォーマンスが低下するテーブル。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
