---
title: 「MDVA-38270：顧客の注文の合計にギフトカードの金額が表示されない」
description: MDVA-38270 パッチは、お客様の注文の合計金額にギフトカードの金額が見つからない場合の問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.0.25 がインストールされている場合に利用できます。 パッチ ID は MDVA-38270。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。
exl-id: 4ab315c4-d26e-4270-a556-66601d01fb2e
feature: Gift, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# MDVA-38270：お客様の注文の合計金額にギフト カードの金額が表示されない

MDVA-38270 パッチは、お客様の注文の合計金額にギフトカードの金額が見つからない場合の問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.25 がインストールされています。 パッチ ID は MDVA-38270。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
クラウドインフラストラクチャー上のAdobe Commerce 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**
Adobe Commerce（すべてのデプロイメント方法） 2.4.1-2.4.2-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ギフト カード金額が注文の合計応答にありません。

<u>前提条件</u>:

1. 顧客アカウントを作成します。
1. ギフトカードを使用して注文する（ギフトカードは注文全体をカバーします）。

<u>再現手順</u>:

顧客、注文、品目、合計に対して顧客クエリを作成します。

```GraphQL
query {
  customer {
    orders(
      pageSize: 20
    ) {
      items {
        id
        order_date
        total {
          grand_total {
            value
            currency
          }
          total_giftcard {
              applied_balance {
                value
                currency
              }
              code
              current_balance {
                value
                currency
              }
              expiration_date
          }
        }
        status
      }
    }
  }
}
```

<u>期待される結果</u>:

`total_giftcard` フィールドを使用できます。

<u>実際の結果</u>:

ギフト カードに関連するフィールドはありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html).
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html).

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md).
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md).

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
