---
title: 「ACSD-46192:async/bulk/V1/configurable-products/bySku/options エンドポイントの問題」
description: ACSD-46192 パッチは、「async/bulk/V1/configurable-products/bySku/options」エンドポイントの問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.19 がインストールされている場合に利用できます。 パッチ ID は ACSD-46192 です。 この問題はAdobe Commerce 2.4.5 で修正されました。
exl-id: fed49708-868a-48ec-8dbc-638d75506a40
feature: Configuration, Products
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# ACSD-46192:async/bulk/V1/configurable-products/bySku/options エンドポイントの問題

ACSD-46192 パッチは、`async/bulk/V1/configurable-products/bySku/options` エンドポイントの問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.19 がインストールされている場合に使用できます。 パッチ ID は ACSD-46192 です。 この問題はAdobe Commerce 2.4.5 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.6 - 2.4.4-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 および 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

POSTリクエストが `async/bulk/V1/configurable-products/bySku/` に送信されると、エラーが発生します。

<u> 再現手順 </u>:

1. `async/bulk/V1/configurable-products/bySku/` にPOSTリクエストを送信します。

```JSON
[{
  "sku": "MS-Champ",
  "option": {
    "attribute_id": "141",
    "label": "Size",
    "position": 0,
    "is_use_default": true,
    "values": [
      {
        "value_index": 9
      }
    ]
  }
}]
```

<u> 期待される結果 </u>:

エラーはありません。 次の応答が返されます。

```JSON
{
  "bulk_uuid": "e5a94361-e16e-432b-a000-c1351a0d01b3",
  "request_items": [
    {
      "id": 0,
      "data_hash": "3e7369ffc0a1602c1f25601a2e11b130f65fd01e68b5091ad746d0cac5b7f35d",
      "status": "accepted"
    }
  ],
  "errors": false
}
```

<u> 実際の結果 </u>:

次のエラーが発生します。

```PHP
TypeError: Argument 3 passed to Magento\Framework\Webapi\ServiceInputProcessor::process() must be of the type array, string given, called in /var/www/html/vendor/magento/module-webapi-async/Controller/Rest/Asynchronous/InputParamsResolver.php on line 154 and defined in /var/www/html/vendor/magento/framework/Webapi/ServiceInputProcessor.php:172
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
