---
title: 「MDVA-35356：一部請求済みの注文をキャンセルした後の店舗のクレジット返品が間違っています」
description: MDVA-35356 パッチは、部分的に請求された注文のキャンセル後に、誤ったストアクレジット返品の問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.19 がインストールされている場合に利用できます。 パッチ ID は MDVA-35356。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。
exl-id: af37f318-0818-4393-b768-939f08b73847
feature: Invoices, Orders, Returns
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# MDVA-35356：一部請求済みの注文をキャンセルした後の店舗クレジット返品が間違っています

MDVA-35356 パッチは、部分的に請求された注文のキャンセル後に、誤ったストアクレジット返品の問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.19 がインストールされている場合に使用できます。 パッチ ID は MDVA-35356。 この問題は、Adobe Commerce バージョン 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.4.1 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 再現手順 </u>:

1. 3 つのシンプルな製品を作成します。
1. 新しいユーザーを作成し、ストアクレジットを割り当てます（例：ストアクレジット = *$10,* 単純な製品価格= *$100*、*$200* および *$300*）。
1. 上記のユーザーでログインし、3 つの製品を買い物かごに追加します。
1. 買い物かごにある 3 つの商品をチェックアウトし、注文の一部にストアクレジットを利用します（例：**小切手/マネーオーダー** で支払われた）。
1. API 経由で注文に対して 2 つの請求書（1 つは製品 1 に対して、もう 1 つは製品 2 に対して）を実行します。

   ```php
   //endpoint POST {\{baseUrl}}/V1/order/:orderId/invoice    //1st API call:    {    "capture": true,    "items": [    {    "order_item_id": 1,    "qty": 1    }    ],    "notify": true,    "appendComment": false    }    //2nd API call:    {    "capture": true,    "items": [    {    "order_item_id": 2,    "qty": 1    }    ],    "notify": true,    "appendComment": false    }
   ```

1. ストアクレジットが最初の請求書に完全に適用されます。
1. &#x200B;店舗クレジット残高= *0 です*。
1. 注文をキャンセルし、2 つの品目が請求され、3 番目の品目がキャンセルされていることを確認します。
1. 店舗のクレジット残高を確認します。

<u> 期待される結果 </u>:

$10 の店舗クレジットが請求されているため、店舗クレジット残高はまだ 0 です。

<u> 実際の結果 </u>:

店舗全体のクレジットが返されます。残高は 10 ドルです。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
