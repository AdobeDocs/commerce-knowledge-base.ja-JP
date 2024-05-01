---
title: 「ACSD-55381：設定可能な製品オプション ID を B2B 購買依頼リストからリクエストする際の解決エラー」
description: ACSD-55381 パッチを適用すると、B2B 要求リストの「configurable_product_option_uid」および「configurable_product_option_value_uid」フィールドに対するGraphQL クエリ中に内部サーバーエラーが発生するAdobe Commerceの問題を修正できます。
feature: GraphQL, B2B, Products
role: Admin, Developer
exl-id: 4e7edb8d-8be8-45c9-b9ba-ff329656312e
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# ACSD-55381:B2B 購買依頼リストから設定可能な製品オプション UID を要求する際のエラーの解決

ACSD-55381 パッチでは、のGraphQL クエリ中に内部サーバーエラーが発生する問題を修正しています。 `configurable_product_option_uid` および `configurable_product_option_value_uid` b2B 購買依頼リストのフィールド。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.42 がインストールされています。 パッチ ID は ACSD-55381 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

クエリ中に内部サーバーエラーが発生しました `configurable_product_option_uid` および `configurable_product_option_value_uid` GraphQLを介した B2B 購買依頼リストのフィールド。

<u>前提条件</u>:

1. Adobe Commerce B2B モジュールがインストールされ、有効になっています。
1. 構成で購買依頼リストが有効化されます。

<u>再現手順</u>:

1. ストアフロントで顧客としてログインします。
1. 構成可能な製品を購買依頼リストに追加します。
1. 次の値を取得してみてください `configurable_product_option_uid` および `configurable_product_option_value_uid` を使用したフィールド `getRequisitionList` GraphQL呼び出しでの関数。

```
query getRequisitionList {
  customer {
    requisition_lists(filter: { uids: { eq: "MQo=" } }) {
      items {
        items(pageSize: 1, currentPage: 1) {
          items {
            ... on ConfigurableRequisitionListItem {
              configurable_options {
                value_id
                id
                configurable_product_option_uid
                configurable_product_option_value_uid
              }
            }
          }
        }
      }
    }
  }
}
```

<u>期待される結果</u>:

```
{
    "data": {
        "customer": {
            "requisition_lists": {
                "items": [
                    {
                        "items": {
                            "items": [
                                {
                                    "configurable_options": [
                                        {
                                            "value_id": 175,
                                            "id": 186,
                                            "configurable_product_option_uid": "MTg2",
                                            "configurable_product_option_value_uid": "MTc1"
                                        },
                                        {
                                            "value_id": 58,
                                            "id": 93,
                                            "configurable_product_option_uid": "OTM=",
                                            "configurable_product_option_value_uid": "NTg="
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                ]
            }
        }
    }
}
```

<u>実際の結果</u>:

エラーが発生しました。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
