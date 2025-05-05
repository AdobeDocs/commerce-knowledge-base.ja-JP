---
title: 「MDVA-44562：見積もり品目の店舗 ID が既定の店舗 ID によって上書きされました」
description: MDVA-44562 パッチでは、デフォルトのストア ID がGraphQL リクエストの見積もり品目のストア ID を上書きする問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.16 がインストールされている場合に利用できます。 パッチ ID は MDVA-44562。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: 902bfc05-411d-4a6c-a6e8-cd7376629b0c
feature: Quotes
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# MDVA-44562：見積品目の店舗 ID が既定の店舗 ID によって上書きされました

MDVA-44562 パッチでは、デフォルトのストア ID がGraphQL リクエストの見積もり品目のストア ID を上書きする問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.16 がインストールされている場合に使用できます。 パッチ ID は MDVA-44562。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

見積もり品目の店舗 ID は、GraphQL リクエストのデフォルトの店舗 ID によって上書きされます。

<u> 再現手順 </u>:

1. 新しいストア表示を作成します。
1. ストア表示ごとに異なる名前で、新しいシンプルな製品を作成します。
1. 顧客を新規作成します。
1. 顧客認証トークンを取得します。

   ```GraphQL
    POST /rest/all/V1/integration/customer/token
    {
      "username": "test@example.com",
      "password": "password"
     }
   ```

1. 認証トークンを使用して、顧客の新しい見積もりを作成します。

   ```GraphQL
   POST rest/default/V1/carts/mine
   ```

1. 商品を買い物かごに追加します。

   ```GraphQL
   POST /rest/default/V1/carts/mine/items
   {
     "cartItem": {
       "sku": "simple1",
       "qty": 1,
       "quote_id": "1"
     }
   }
   ```

1. デフォルトのストア表示に対応する買い物かごの内容を取得します。

   ```GraphQL
   GET rest/default/V1/carts/mine/
   ```

1. 新しいストア表示の買い物かごコンテンツを取得します。

   ```GraphQL
   GET rest/<store_view_2>/V1/carts/mine/
   ```

<u> 期待される結果 </u>:

新しいストア表示からの応答には、新しいストア表示の製品名が表示されます。

<u> 実際の結果 </u>:

新しいストア表示からの応答では、デフォルトのストア表示に製品名の設定が表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) を参照してください。
