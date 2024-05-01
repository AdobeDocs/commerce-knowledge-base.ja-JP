---
title: 「ACSD-55414:MariaDB が entitys_ids をキャストしようとすると、パフォーマンスが低下します」
description: MariaDB が「entitys_ids」を文字列から整数に変換しようとすると、インデックス再作成のパフォーマンスが妨げられ、Adobe Commerceの問題を修正するために ACSD-55414 パッチを適用してください。
feature: Attributes
role: Admin, Developer
exl-id: 008a4fda-5d80-47e2-8fb4-c1e39d15a6ba
source-git-commit: 35cd21581ee34a6213be42a79e159439b8856fb6
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# ACSD-55414:MariaDB がパラメーターをキャストしようとするとパフォーマンスが低下します `entitys_ids`

ACSD-55414 パッチは、MariaDB が変換を試みたときにインデックス再作成のパフォーマンスが妨げられる問題を修正します `entitys_ids` 文字列から整数へ。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.41 がインストールされています。 パッチ ID は ACSD-55414 です。 この問題はAdobe Commerce 2.4.6 で修正されていることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5-p5

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

MariaDB がインデックスをキャストしようとすると、インデックス再作成のパフォーマンスが妨げられます `entitys_ids` 文字列から整数へ。

<u>再現手順</u>:

1. 更新 `setup/performance-toolkit/profiles/ce/small.xml` を設定することによって *50000* シンプルな製品。
1. 次のコマンドを実行して、このプロファイルを生成します。 `bin/magento setup:perf:generate-fixtures setup/performance-toolkit/profiles/ce/small.xml`.
1. 再インデックスを実行します。 `bin/magento indexer:reindex catalog_product_attribute`.

<u>期待される結果</u>:

再インデックスの完了には十分な時間がかかります。

<u>実際の結果</u>:

この再インデックスの完了に時間がかかりすぎます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
