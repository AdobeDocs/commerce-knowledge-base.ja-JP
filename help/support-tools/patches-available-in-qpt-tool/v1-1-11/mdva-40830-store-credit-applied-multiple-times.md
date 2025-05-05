---
title: 「MDVA-40830：注文中に店舗クレジットが複数回適用される」
description: MDVA-40830 パッチにより、注文の発注時にストア クレジットが複数回適用される問題が修正されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.11 がインストールされている場合に利用できます。 パッチ ID は MDVA-40830。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 218a100a-4500-4ef5-bbdb-fbbd12f2fa26
feature: Orders, Returns
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# MDVA-40830：注文中に店舗クレジットが複数回適用される

MDVA-40830 パッチにより、注文の発注時にストア クレジットが複数回適用される問題が修正されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.11 がインストールされている場合に使用できます。 パッチ ID は MDVA-40830。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.3.7-p2、2.4.0 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

店舗クレジットは、発注時に複数回適用されます。

<u> 再現手順 </u>:

1. 顧客を作成し、顧客アカウントにストアクレジットを追加します。
1. シンプルな製品を買い物かごに追加します。
1. 買い物かごの出荷先住所と請求先住所を設定します。
1. 買い物かごの総計を確認します。
1. 次のGraphQL リクエストを使用して、買い物かごにストアクレジットを適用します。

<pre>
<code class="language-graphql">
mutation &lbrace;
  applyStoreCreditToCart(
    input: { cart_id: "%cartId%" }
  ) &lbrace;
    cart &lbrace;
      prices &lbrace;
        grand_total &lbrace;
          currency
          value
        &rbrace;
      &rbrace;
      applied_store_credit &lbrace;
        applied_balance &lbrace;
          currency
          value
        &rbrace;
        current_balance &lbrace;
          currency
          value
        &rbrace;
      &rbrace;
    &rbrace;
  &rbrace;
&rbrace;
</code>
</pre>

<u> 期待される結果 </u>:

applied_store_credit の値は正確に適用され、買い物かごの合計は API 応答に正しく反映されます。

<u> 実際の結果 </u>:

applied_store_credit の値は 2 回適用され、cart と grand_total の両方に影響を与えます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
