---
title: 「MDVA-31640 パッチ：REST API を使用して連続するスケジュールされた更新を作成できない」
description: MDVA-31640 パッチは、更新開始日が以前の既存の更新の終了日と一致する場合、REST API を使用して複数のストアに対して特別価格の新しいスケジュールされた更新を作成できない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.9 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。
exl-id: 8d91db3d-7c94-4757-8087-4cf53cad81e7
feature: REST
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---

# MDVA-31640 パッチ：REST API を介して連続するスケジュールされた更新を作成できない

MDVA-31640 パッチは、更新開始日が以前の既存の更新の終了日と一致する場合、REST API を使用して複数のストアに対して特別価格の新しいスケジュールされた更新を作成できない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.9 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用にパッチが作成されました。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.1 - 2.3.5-p2、2.4.0、2.4.0-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

更新の開始日が以前の既存の更新の終了日と一致する場合、REST API を使用して複数のストアに対して特別価格の新しいスケジュールされた更新を作成できない問題を修正しました。

<u> 再現手順 </u>:

1. 追加の web サイト、ストア、ストア表示を設定します。
1. 「product1」と「product2」という 2 つのシンプルな製品を作成します。
1. product1 を 1 つの web サイトに、product2 を両方の web サイトに割り当てます。
1. ID 1 を持つストアのストア表示で、product1 の特別価格のスケジュールされた更新を作成します。 REST API `POST` リクエストを使用して、次のペイロードで `rest/V1/products/special-price` を実行します。
   `{        "prices": [            {                "price": 15,                "store_id": 1,                "sku": "product1",                "price_from": "2021-11-15 04:00:00",                "price_to": "2021-11-15 04:10:00"            }        ]    }`
1. REST API `POST` リクエストを使用して、ID 1 と 2 のストアの両方のストアビューで、product2 の特別価格のスケジュールされた更新を、次のペイロードで `rest/V1/products/special-price` 行します（`price_from` 日は前のリクエストの `price_to` 日と同じです）。
   `{        "prices": [            {                "price": 14,                "store_id": 1,                "sku": "product2",                "price_from": "2021-11-15 04:10:00",                "price_to": "2021-11-15 04:15:00"            },            {                "price": 13,                "store_id": 2,                "sku": "product2",                "price_from": "2021-11-15 04:10:00",                "price_to": "2021-11-15 04:15:00"            }        ]    }`

<u> 期待される結果 </u>:

特別な価格変更を含むスケジュールされた更新は、両方のストアビューで作成されます。

<u> 実際の結果 </u>:

Adobe Commerceがエラーをスローする。 スケジュールされた更新は作成されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
