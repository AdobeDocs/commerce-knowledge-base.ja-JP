---
title: 'ACSD-50817: cron ジョブ sales_clean_quotes を最適化して実行速度を向上'
description: ACSD-50817 パッチを適用して、見積もりテーブルの「store_id」列と「updated_at」列に複合インデックスを追加することで、cron ジョブ「sales_clean_quotes」を最適化し、より高速に実行できるようにします。
exl-id: b08b12ff-37ac-4a7d-bce2-2a27e4f916f0
feature: Quotes
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# ACSD-50817: cron ジョブを最適化する `sales_clean_quotes` より速く実行するには

ACSD-50817 パッチは、cron ジョブを最適化します `sales_clean_quotes` に複合インデックスを追加してより高速に実行するには、次の手順に従います `store_id` および `updated_at` 引用符表の列。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.31 がインストールされています。 パッチ ID は ACSD-50817 です。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Cron ジョブ `sales_clean_quotes` が遅すぎる。 このパッチでは、に複合インデックスを追加することで実行を高速化するように最適化されています。 `store_id` および `updated_at` 引用符表の列。

<u>再現手順</u>:

1. 50～80,000 万件の引用符を生成する `updated_at` を 30 日未満の期間として設定します。
1. cron ジョブの実行 `sales_clean_quotes` または、見積もりテーブルに対する次のクエリを実行します。

   ```cron
   SELECT COUNT(*) FROM `quote` AS `main_table` WHERE (`store_id` = '1') AND (`updated_at` <= '2023-02-25') AND (`is_persistent` = '0')
   
   SELECT * FROM `quote` AS `main_table` WHERE (`store_id` = '1') AND (`updated_at` <= '2023-02-25') AND (`is_persistent` = '0') LIMIT 50
   ```

<u>期待される結果</u>

Cron ジョブ `sales_clean_quotes` は、に複合インデックスを追加することでより高速に実行するように最適化されます。 `store_id` および `updated_at` 引用符表の列。

<u>実際の結果</u>

クエリが遅すぎます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
