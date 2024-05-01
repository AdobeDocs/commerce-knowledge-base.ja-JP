---
title: 「MDVA-44505：報酬ポイントを適用する買い物かごに対するGraphQL クエリで総計が更新されない」
description: MDVA-44505 パッチは、報酬ポイントを適用する買い物かごに対するGraphQL クエリが報酬ポイントを考慮せず、誤った総計を返す問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.14 がインストールされている場合に利用できます。 パッチ ID は MDVA-44505。 この問題はAdobe Commerce 2.4.3 で修正されました。
exl-id: 724273ba-b020-4dba-88ae-94968bbd83de
feature: GraphQL, Orders, Rewards, Shopping Cart
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# MDVA-44505：報酬ポイントを適用する買い物かごに対するGraphQL クエリで総計が更新されない

MDVA-44505 パッチは、報酬ポイントを適用する買い物かごに対するGraphQL クエリが報酬ポイントを考慮せず、誤った総計を返す問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.14 がインストールされています。 パッチ ID は MDVA-44505。 この問題はAdobe Commerce 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1 ～ 2.4.2-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

報酬ポイントを適用する買い物かごに対するGraphQL クエリは報酬ポイントを考慮せず、誤った総計を返します。

<u>再現手順</u>:

1. 報酬ポイントを設定します。
1. 買い物かごを作成して、報酬ポイントを適用します。
1. を呼び出します `GetCart` からのクエリ `GraphQL` エンドポイントを設定して買い物かごを取得します。

   ```GraphQL
   query {
     cart(cart_id: "{CART_ID}") {
       prices {
         discounts {
           amount {
             value
           }
         }
         grand_total {
           value
         }
       }
     }
   }
   ```

1. 総計のエントリを確認します。
1. 次に、REST API を使用して、顧客の買い物かごの合計を確認します（`/rest/V1/carts/mine/totals`）に設定します。

<u>期待される結果</u>:

買い物かごに対するGraphQL クエリは、報酬ポイントを考慮した正しい総計を返します。

<u>実際の結果</u>:

GraphQLのクエリで報酬ポイントが考慮されず、誤った総計が返されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
