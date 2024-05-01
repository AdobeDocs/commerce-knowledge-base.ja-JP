---
title: 「MDVA-15546：句があいまいな列'entity_id'」
description: 「MDVA-15546 パッチは、一部のAmazon拡張機能に関連する可能性のあるパフォーマンスの問題を解決します。 この問題は、例外ログに次のエラーで示されています。*where* *Column 'entity\\_id' in where 句があいまいな場合、クエリは次のとおりです：SELECT \\'main\\\_table\\'。\\*, \\'extension\\_attribute\\_amazon\\_order\\_reference\\_id* \\'. このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.20 がインストールされている場合に利用できます。 パッチ ID は MDVA-15546 です。」
exl-id: d58c1728-eb7a-49e8-a329-3197f2339b9c
feature: B2B, Commerce Intelligence
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# MDVA-15546：句があいまいな列&#39;entity_id&#39;

MDVA-15546 パッチは、一部のAmazon拡張機能に関連する可能性のあるパフォーマンスの問題を解決します。 この問題は、の例外ログに次のエラーで示されます。 *ここで、*   *句があいまいな場合のカラム &#39;entity\_id&#39;、クエリは次のとおりです：SELECT \&#39;main\_table\&#39;\*, \&#39;extension\_attribute\_amazon\_order\_reference\_id* \&#39;。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.20 がインストールされています。 パッチ ID は MDVA-15546。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.2.5 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.0 - 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

一部のAmazon拡張機能に関連する可能性のあるパフォーマンスの問題。

<u>前提条件</u>:

B2B とAmazon\_Payment でAdobe Commerceをクリーンアップします。

<u>再現手順</u>:

1. ストアフロントページに移動します。
1. 商品を買い物かごに追加します。
1. Cron ジョブを待つかトリガーします。 `flush_preview_quotas`.

<u>実際の結果</u>:

チェック時 `var/log/exception/log`には、次のエラーが表示されます。

*`report.ERROR: Cron Jobflush_preview_quotashas an error: SQLSTATE[23000]: Integrity constraint violation: 1052 Column 'entity_id' in where clause is ambiguous, query was: SELECT `main_table`.*, `extension_attribute_amazon_order_reference_id`.`amazon_order_reference_id` AS `extension_attribute_amazon_order_reference_id_amazon_order_reference_id`, `extension_attribute_amazon_order_reference_id`.`quote_id` AS `extension_attribute_amazon_order_reference_id_quote_id`, `extension_attribute_amazon_order_reference_id`.` sandbox_simulation_reference` AS `extension_attribute_amazon_order_reference_id_sandbox_simulation_reference`, `extension_attribute_amazon_order_reference_id`.`確認済み` AS `extension_attribute_amazon_order_reference_id_confirmed` FROM `見積もり` AS `main_table` LEFT JOIN `amazon_quote` AS `extension_attribute_amazon_order_reference_id` ON main_table.entity_id = extension_attribute_amazon_order_reference_id.quote_id WHERE ...`*

<u>期待される結果</u>:

Cron ジョブがエラーなしで完了する。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
