---
title: 「MDVA-36572：クレジット メモの更新後に作成された新しい在庫引当」
description: MDVA-36572 パッチは、クレジット メモの更新後に新しい在庫予約が作成される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.0.25 がインストールされている場合に利用できます。 パッチ ID は MDVA-36572。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 6d98e1aa-0faf-4317-a6ae-386f84266b9c
feature: Inventory, Orders, Returns
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# MDVA-36572: クレジット・メモの更新後に作成された新規在庫引当


## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
クラウドインフラストラクチャー 2.4.1 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメントタイプ） 2.3.5-2.4.2-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

クレジットメモ予約更新オブザーバーは、クレジットメモが更新されるたびにトリガーされます。 発注との契約に従い、作成されたクレジット・メモでのみトリガーされるように予約更新のロジックが変更されました。 API を介したクレジットメモの編集の可能性は、PO によっても個別のチケットの範囲で確認されます。

<u>再現手順</u>:

1. 顧客アカウントを作成します。
1. シンプルな製品を作成します。
1. 注文の新しい注文、請求書、およびクレジット メモを作成します。
1. 新しい統合を作成します。
1. inventory_reservation テーブルを確認します。

   ```SQL
       select * from inventory_reservation;
       +----------------+----------+----------+----------+-------------------------------------------------------------------------------------------------------------+
       | reservation_id | stock_id | sku      | quantity | metadata                                                                                                    |
       +----------------+----------+----------+----------+-------------------------------------------------------------------------------------------------------------+
       |              1 |        1 | simple_1 |  -1.0000 | {"event_type":"order_placed","object_type":"order","object_id":"","object_increment_id":"000000001"}        |
       |              2 |        1 | simple_1 |   1.0000 | {"event_type":"creditmemo_created","object_type":"order","object_id":"1","object_increment_id":"000000001"} |
       +----------------+----------+----------+----------+-------------------------------------------------------------------------------------------------------------+
       2 rows in set (0.00 sec)
   ```

1. GET要求の送信先： `../rest/default/V1/creditmemo/3`
1. 応答をコピー（例）:

   ```JSON
       {
       "adjustment": 0,
       "adjustment_negative": 0,
       "adjustment_positive": 0,
       "base_adjustment": 0,
       "base_adjustment_negative": 0,
       "base_adjustment_positive": 0,
       "base_currency_code": "USD",
       "base_discount_amount": 0,
       "base_grand_total": 105,
       "base_discount_tax_compensation_amount": 0,
       "base_shipping_amount": 5,
       "base_shipping_incl_tax": 5,
       "base_shipping_tax_amount": 0,
       "base_subtotal": 100,
       "base_subtotal_incl_tax": 100,
       "base_tax_amount": 0,
       "base_to_global_rate": 1,
       "base_to_order_rate": 1,
       "billing_address_id": 2,
       "created_at": "2021-04-05 23:43:45",
       "discount_amount": 0,
       "entity_id": 1,
       "global_currency_code": "USD",
       "grand_total": 105,
       "discount_tax_compensation_amount": 0,
       "increment_id": "000000001",
       "order_currency_code": "USD",
       "order_id": 1,
       "shipping_address_id": 1,
       "shipping_amount": 5,
       "shipping_incl_tax": 5,
       "shipping_tax_amount": 0,
       "state": 2,
       "store_currency_code": "USD",
       "store_id": 1,
       "store_to_base_rate": 0,
       "store_to_order_rate": 0,
       "subtotal": 100,
       "subtotal_incl_tax": 100,
       "tax_amount": 0,
       "updated_at": "2021-04-05 23:43:45",
       "items": [
        {
            "base_cost": null,
            "base_discount_tax_compensation_amount": 0,
            "base_price": 100,
            "base_price_incl_tax": 100,
            "base_row_total": 100,
            "base_row_total_incl_tax": 100,
            "base_tax_amount": 0,
            "base_weee_tax_row_disposition": 0,
            "entity_id": 1,
            "discount_tax_compensation_amount": 0,
            "name": "simple_1",
            "order_item_id": 1,
            "parent_id": 1,
            "price": 100,
            "price_incl_tax": 100,
            "product_id": 1,
            "qty": 1,
            "row_total": 100,
            "row_total_incl_tax": 100,
            "sku": "simple_1",
            "tax_amount": 0,
            "weee_tax_applied": "[]",
            "weee_tax_applied_row_amount": 0,
            "weee_tax_row_disposition": 0
        }
       ],
       "comments": []
      }
   ```

1. POST要求の送信先： `../rest/default/V1/creditmemo`

   ```JSON
       {
       "entity":
        --paste full response from previous step here--
       }
   ```

   >[!NOTE]
   >
   >このようなペイロードは再生を簡素化するためにのみ使用されます。顧客はカスタム属性を更新した後で同じ問題が発生します

1. inventory_reservation テーブルを確認します。

<u>実際の結果</u>:

```sql
select * from inventory_reservation;
+----------------+----------+----------+----------+-------------------------------------------------------------------------------------------------------------+
| reservation_id | stock_id | sku      | quantity | metadata                                                                                                    |
+----------------+----------+----------+----------+-------------------------------------------------------------------------------------------------------------+
|              1 |        1 | simple_1 |  -1.0000 | {"event_type":"order_placed","object_type":"order","object_id":"","object_increment_id":"000000001"}        |
|              2 |        1 | simple_1 |   1.0000 | {"event_type":"creditmemo_created","object_type":"order","object_id":"1","object_increment_id":"000000001"} |
|              3 |        1 | simple_1 |   1.0000 | {"event_type":"creditmemo_created","object_type":"order","object_id":"1","object_increment_id":"000000001"} |
+----------------+----------+----------+----------+-------------------------------------------------------------------------------------------------------------+
3 rows in set (0.00 sec)
```

<u>期待される結果</u>:

同じクレジット メモの 2 番目の予約は作成されません。

## パッチの適用

個々のパッチを適用するには、デプロイメントタイプに応じて次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md).
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md).

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
