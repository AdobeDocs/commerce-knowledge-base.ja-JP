---
title: 「MDVA-37288:GraphQL リクエスト後に返された階層価格が正しくない」
description: Adobe Commerce用の MDVA-37288 品質パッチは、GraphQL リクエスト後に誤った階層価格が返される問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） v.1.0.23 がインストールされている場合に利用できます。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。
exl-id: d2cf24d5-6163-4968-a89c-b7407d439e1c
feature: GraphQL, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# MDVA-37288:GraphQL リクエスト後に返された階層価格が間違っている

Adobe Commerce用の MDVA-37288 品質パッチは、GraphQL リクエスト後に誤った階層価格が返される問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) v.1.0.23 がインストールされている。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

* このパッチは、クラウドインフラストラクチャ 2.4.2 上のAdobe Commerce用に設計されました
* このパッチは、Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.4.2 とも互換性があります

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

1. 任意の項目に階層の価格を追加します（この例では、id=1 および id=2 の項目に階層の価格が追加されています）。
1. 階層価格のある商品と階層価格のない商品を含む検索でGraphQL クエリを実行します。

<pre><code class="language-graphql">
{
  products(pageSize: 20, currentPage: 1, search: "24-MB0") {
    items {
      id
      price_tiers {
        quantity
        final_price {
          value
        }
      }
    }
  }
}
</code></pre>

<u>期待される結果</u>:

階層価格を持つ項目のみが適切な階層価格を返す必要があります。

```json
{
  "data": {
        "products": {
            "items": [
                {
                    "id": 17,
                    "price_tiers": []
                },
                {
                    "id": 1,
                    "price_tiers": [
                        {
                            "quantity": 1,
                            "final_price": {
                                "value": 34
                            }
                        },
                        {
                            "quantity": 5,
                            "final_price": {
                                "value": 32
                            }
                        }
                    ]
                },
                {
                    "id": 23,
                    "price_tiers": []
                },
                {
                    "id": 19,
                    "price_tiers": []
                }
            ]
        }
    }
}
```

<u>実際の結果</u>:

* 階層価格のアイテムの後に来るすべてのアイテムには、応答で階層価格が設定されます。
* 返される階層の価格データは、階層の価格が設定されたループ内の最後の項目のものです。

応答の例：

```json
{
    "data": {
        "products": {
            "items": [
                {
                    "id": 17,
                    "price_tiers": []
                },
                {
                    "id": 1,
                    "price_tiers": [
                        {
                            "quantity": 1,
                            "final_price": {
                                "value": 34
                            }
                        },
                        {
                            "quantity": 5,
                            "final_price": {
                                "value": 32
                            }
                        }
                    ]
                },
                {
                    "id": 23,
                    "price_tiers": [
                        {
                            "quantity": 1,
                            "final_price": {
                                "value": 34
                            }
                        },
                        {
                            "quantity": 5,
                            "final_price": {
                                "value": 32
                            }
                        }
                    ]
                },
                {
                    "id": 19,
                    "price_tiers": [
                        {
                            "quantity": 1,
                            "final_price": {
                                "value": 34
                            }
                        },
                        {
                            "quantity": 5,
                            "final_price": {
                                "value": 32
                            }
                        }
                    ]
                }
            ]
        }
    }
}
```


## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、開発者向けドキュメントの以下のリンクを使用します。

* Adobe CommerceとMagento Open Sourceのオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html)

## 関連資料

サポートナレッジベースの品質向上パッチツールについて詳しくは、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節（サポートナレッジベース）を参照してください。
