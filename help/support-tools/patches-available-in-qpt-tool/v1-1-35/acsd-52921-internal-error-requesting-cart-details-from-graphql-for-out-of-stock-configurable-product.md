---
title: 「ACSD-52921：設定可能な在庫切れの商品について、GraphQLに買い物かごの詳細をリクエスト中にエラーが発生しました」
description: ACSD-52921 パッチを適用すると、設定可能な在庫切れの商品についてGraphQLに買い物かごの詳細をリクエストしたときに内部エラーが発生するAdobe Commerceの問題を修正できます。
feature: GraphQL, Configuration, Products, Shopping Cart
role: Admin
exl-id: 687460c4-f0d5-45d2-82b1-dda2947fe1e7
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# ACSD-52921：設定可能な在庫切れの商品について、GraphQLにカートの詳細をリクエスト中にエラーが発生しました

ACSD-52921 パッチでは、設定可能な在庫切れの商品について、GraphQLに買い物かごの詳細をリクエストすると内部エラーが発生する問題を修正しました。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.35 がインストールされている場合に使用できます。 パッチ ID は ACSD-52921 です。 この問題はAdobe Commerce 2.4.7 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

在庫切れの設定可能な商品の買い物かごの詳細をGraphQLにリクエストすると、内部エラーが発生します。

<u> 再現手順 </u>:

1. いくつかのオプションを使用して設定可能な製品を作成します。
1. 上記の設定可能な製品のオプションをフロントエンド（ゲストのチェックアウト）から買い物かごに追加します。
1. 上記で作成した引用の `[ masked_id ]` を `[ quote_id_mask ]` db テーブルから取得します。
1. 次のGraphQL クエリを実行して、上記のゲストの買い物かごの詳細を取得します。

   手順 3 で取得した `[ masked_id ]` をクエリに追加します。

   ```GraphQL
   {
       cart(cart_id: "masked_id") {
           items {
               product {
                   name
                   sku
               }
               ... on ConfigurableCartItem {
                   configurable_options {
                       configurable_product_option_uid
                       option_label
                       configurable_product_option_value_uid
                       value_label
                   }
               }
               quantity
               errors {
                   code
                   message
               }
           }
       }
   }   
   ```

1. これにより、問題なく見積もりの詳細が返されます。
1. バックエンドに移動し、設定可能な製品の *[!UICONTROL Stock Status]* を *[!UICONTROL Out of Stock]* に更新します。
1. 手順 4 と同じGraphQL クエリを実行します。

<u> 期待される結果 </u>:

このエラーメッセージは、応答で正しく送信または処理されます。

<u> 実際の結果 </u>:

*500 内部サーバー* GraphQL クエリへの応答でエラーがスローされる。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
