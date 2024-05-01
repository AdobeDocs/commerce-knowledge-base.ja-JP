---
title: 「MDVA-43348：ギフトカードのGraphQL リクエストでエラーが表示される」
description: MDVA-43348 パッチは、「gift_card_options」に「uid」が含まれている場合にギフトカードのGraphQL リクエストがエラーを示す問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.12 がインストールされている場合に利用できます。 パッチ ID は MDVA-43348。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: a9c0e1da-6698-463a-a6a8-60522f029b53
feature: Gift, GraphQL
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# MDVA-43348：ギフトカードのGraphQLリクエストにエラーが表示される

MDVA-43348 パッチは、次の場合にギフトカードのGraphQL リクエストにエラーが表示される問題を修正します `gift_card_options` 「uid」を含めます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.12 がインストールされています。 パッチ ID は MDVA-43348。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

gift_card_options に「uid」が含まれている場合、ギフトカードのGraphQL リクエストにエラーが表示されます。

<u>再現手順</u>:

1. ギフトカード製品を作成します。
1. 再インデックスを実行します。
1. URL キーが「gift-card」であるGraphQL呼び出しを行います。

<pre>
<code class="language-graphql">
query getProductOptionsForProductPage_bypassFastly($urlKey: String!) {
  products(filter: { url_key: { eq: $urlKey } }) {
    items {
      id
      url_key
      ... on GiftCardProduct {
        allow_open_amount
        open_amount_min
        open_amount_max
        giftcard_type
        is_redeemable
        lifetime
        allow_message
        message_max_length
        gift_card_options {
          uid
          title
          required
        }
      }
    }
  }
}
</code>
</pre>

<u>期待される結果</u>:

ギフトカードのデータは、リクエストに応じて返されます。

<u>実際の結果</u>:

ギフト カードのデータを要求すると、次のエラーが発生します。

<pre>
<code class="language-graphql">
{
  "errors": [
    {
      "debugMessage": "Cannot return null for non-nullable field \"CustomizableFieldOption.uid\".",
      "message": "Internal server error",
      "extensions": {
        "category": "internal"
      },
      "locations": [
        {
          "line": 16,
          "column": 1
        }
      ],
      "path": [
        "products",
        "items",
        0,
        "gift_card_options",
        0,
        "uid"
      ]
    },
    {
      "debugMessage": "Cannot return null for non-nullable field \"CustomizableFieldOption.uid\".",
      "message": "Internal server error",
      "extensions": {
        "category": "internal"
      },
      "locations": [
        {
          "line": 16,
          "column": 1
        }
      ],
      "path": [
        "products",
        "items",
        0,
        "gift_card_options",
        1,
        "uid"
      ]
    },
    {
      "debugMessage": "Cannot return null for non-nullable field \"CustomizableFieldOption.uid\".",
      "message": "Internal server error",
      "extensions": {
        "category": "internal"
      },
      "locations": [
        {
          "line": 16,
          "column": 1
        }
      ],
      "path": [
        "products",
        "items",
        0,
        "gift_card_options",
        2,
        "uid"
      ]
    },
    {
      "debugMessage": "Cannot return null for non-nullable field \"CustomizableFieldOption.uid\".",
      "message": "Internal server error",
      "extensions": {
        "category": "internal"
      },
      "locations": [
        {
          "line": 16,
          "column": 1
        }
      ],
      "path": [
        "products",
        "items",
        0,
        "gift_card_options",
        3,
        "uid"
      ]
    },
    {
      "debugMessage": "Cannot return null for non-nullable field \"CustomizableFieldOption.uid\".",
      "message": "Internal server error",
      "extensions": {
        "category": "internal"
      },
      "locations": [
        {
          "line": 16,
          "column": 1
        }
      ],
      "path": [
        "products",
        "items",
        0,
        "gift_card_options",
        4,
        "uid"
      ]
    }
  ],
  "data": {
    "products": {
      "items": [
        {
          "id": 2,
          "url_key": "gitf-card",
          "allow_open_amount": false,
          "open_amount_min": null,
          "open_amount_max": null,
          "giftcard_type": "VIRTUAL",
          "is_redeemable": true,
          "lifetime": 0,
          "allow_message": true,
          "message_max_length": 255,
          "gift_card_options": [
            null,
            null,
            null,
            null,
            null
          ]
        }
      ]
    }
  }
}
</code>
</pre>

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
