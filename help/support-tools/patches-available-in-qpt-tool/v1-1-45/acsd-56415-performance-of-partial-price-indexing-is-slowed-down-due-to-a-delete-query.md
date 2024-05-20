---
title: '''ACSD-56415: パフォーマンス [!UICONTROL Partial Price Indexing] 「DELETE」クエリにより速度が低下しました'
description: が次のパフォーマンスを実行するAdobe Commerceの問題を修正するには、ACSD-56415 パッチを適用してください [!UICONTROL Partial Price Indexing] データベースにインデックスに対する部分的な価格データが多数ある場合、「DELETE」クエリが原因で速度が低下します。
feature: Catalog Service
role: Admin, Developer
exl-id: 0b099570-9f27-4ae2-9384-6b69ea50bd98
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# ACSD-56415：のパフォーマンス [!UICONTROL Partial Price Indexing] は、以下の理由で減速します `DELETE` クエリ

ACSD-56415 パッチは、 [!UICONTROL Partial Price Indexing] は、以下の理由により減速しています： `DELETE` データベースに多くの部分価格データインデックスがある場合にクエリします。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.45 がインストールされています。 パッチ ID は ACSD-56023 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

パフォーマンス [!UICONTROL Partial Price Indexing] は、以下の理由により減速しています： `DELETE` データベースに多くの部分価格データインデックスがある場合にクエリします。

<u>再現手順</u>:

1. 作成 *300000 製品* および *10 の Web サイト* 大規模なパフォーマンスプロファイルの使用。
1. 管理パネルにログインします。
1. 作成 *10 の顧客グループ*.
1. 次のクエリを実行して、製品をに追加します `_cl` テーブル：

   ``
    insert into catalog_product_price_cl (entity_id) select entity_id from catalog_product_entity
 ``

1. 次のコマンドを実行して、部分価格インデックス作成プロセスをトリガーします。

   ``
    bin/magento cron:run --group=index --bootstrap=standaloneProcessStarted=1
 ``

<u>期待される結果</u>:

SQL クエリのDELETE `main_table` 送信元 `catalog_product_index_price` は迅速に実行されます。

<u>実際の結果</u>:

SQL クエリのDELETE `main_table` 送信元 `catalog_product_index_price` は非常に低速で実行されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
