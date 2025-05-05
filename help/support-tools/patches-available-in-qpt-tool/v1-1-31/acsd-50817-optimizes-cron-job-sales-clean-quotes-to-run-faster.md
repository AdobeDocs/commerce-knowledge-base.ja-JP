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

# ACSD-50817: Cron ジョブ `sales_clean_quotes` を最適化して実行速度を向上

ACSD-50817 パッチは、見積もりテーブルの `store_id` 列と `updated_at` 列に複合インデックスを追加することで、cron ジョブ `sales_clean_quotes` ータの実行速度を最適化します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.31 がインストールされている場合に使用できます。 パッチ ID は ACSD-50817 です。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

cron ジョブ `sales_clean_quotes` が遅すぎる。 このパッチでは、引用符テーブルの `store_id` 列と `updated_at` 列に複合インデックスを追加することで、より高速に実行するように最適化されています。

<u> 再現手順 </u>:

1. 50～80,000 万件の見積りを生成し、`updated_at` を 30 日未満に設定します。
1. Quote テーブルで cron ジョブ `sales_clean_quotes` または次のクエリを実行します。

   ```cron
   SELECT COUNT(*) FROM `quote` AS `main_table` WHERE (`store_id` = '1') AND (`updated_at` <= '2023-02-25') AND (`is_persistent` = '0')
   
   SELECT * FROM `quote` AS `main_table` WHERE (`store_id` = '1') AND (`updated_at` <= '2023-02-25') AND (`is_persistent` = '0') LIMIT 50
   ```

<u> 期待される結果 </u>

Cron ジョブ `sales_clean_quotes` は、見積もりテーブルの `store_id` 列と `updated_at` 列に複合インデックスを追加することで実行速度を向上させるように最適化されています。

<u> 実績 </u>

クエリが遅すぎます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
