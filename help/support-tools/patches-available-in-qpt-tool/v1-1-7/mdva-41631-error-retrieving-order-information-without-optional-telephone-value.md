---
title: 'MDVA-41631: オプションの"telephone"値なしで注文情報を取得中にエラーが発生しました'
description: MDVA-41631 パッチでは、オプションの「telephone」値を使用せずにGraphQLから注文情報を取得する際にエラーが発生する問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.7 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 94b0b918-c1f9-4f5d-8fcd-8b92a9ca8c59
feature: Orders
role: Admin
source-git-commit: 77f41d6034f985794e5c5b89cc007a69858683b9
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# MDVA-41631: オプションの&quot;telephone&quot;値なしで注文情報を取得中にエラーが発生しました

MDVA-41631 パッチでは、オプションの「telephone」値を使用せずにGraphQLから注文情報を取得する際にエラーが発生する問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.7 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.4.1 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

オプションの「電話」値を使用せずに、GraphQLから注文情報を取得するとエラーが発生します。

<u> 再現手順 </u>:

1. **ストア**/**設定**/**カスタマー**/**カスタマー設定**/**名前と住所のオプション**/**電話を表示** に移動し、電話番号をオプションとして設定します。
1. ログインしているユーザーとしてGraphQL API を使用して注文します。
   * 請求先住所と配送先住所を設定する際は、電話番号を設定しないでください。 アドビの開発者向けドキュメントの [GraphQLのチェックアウトチュートリアル ](https://developer.adobe.com/commerce/webapi/graphql/tutorials/checkout/) に記載されている手順に従います。
1. GraphQL [customerOrders クエリ ](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/queries/orders/) を使用して注文を取得します。

<pre>
<code class="language-graphql">
&lbrace;
  customer &lbrace;
    firstname
    lastname
    suffix
    email

    orders(filter:{number:{eq:"000000001"}})&lbrace;
        items&lbrace;
          billing_address &lbrace;
firstname
lastname
street
city
region
region_id
postcode
telephone
country_code
&rbrace;
shipping_address &lbrace;
firstname
lastname
street
city
region
region_id
postcode
telephone
country_code
&rbrace;
        &rbrace;
    &rbrace;
  &rbrace;
&rbrace;
</code>
</pre>

<u> 期待される結果 </u>:

ユーザーは注文情報を取得します。

<u> 実際の結果 </u>:

ユーザーに次のエラーが表示されます。*&quot;message&quot;: &quot;Internal server error&quot;,*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
