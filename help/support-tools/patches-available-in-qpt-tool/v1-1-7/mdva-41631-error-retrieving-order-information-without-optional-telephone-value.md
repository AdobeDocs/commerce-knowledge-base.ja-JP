---
title: 'MDVA-41631: オプションの"telephone"値なしで注文情報を取得中にエラーが発生しました'
description: MDVA-41631 パッチでは、オプションの「telephone」値を使用せずにGraphQLから注文情報を取得する際にエラーが発生する問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.7 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 94b0b918-c1f9-4f5d-8fcd-8b92a9ca8c59
feature: Orders
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# MDVA-41631: オプションの&quot;telephone&quot;値なしで注文情報を取得中にエラーが発生しました

MDVA-41631 パッチでは、オプションの「telephone」値を使用せずにGraphQLから注文情報を取得する際にエラーが発生する問題が修正されています。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.7 がインストールされています。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.4.1 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

オプションの「電話」値を使用せずに、GraphQLから注文情報を取得するとエラーが発生します。

<u>再現手順</u>:

1. に移動 **ストア** > **設定** > **顧客** > **顧客設定** > **名前と住所のオプション** > **電話を表示** 電話番号をオプションとして設定します。
1. ログインしているユーザーとしてGraphQL API を使用して注文します。
   * 請求先住所と配送先住所を設定する際は、電話番号を設定しないでください。 に記載されている手順に従います [GraphQL チェックアウトチュートリアル](https://devdocs.magento.com/guides/v2.4/graphql/tutorials/checkout/checkout-customer.html) 開発者向けドキュメントを参照してください。
1. GraphQLを使用して注文を取得します [customerOrders クエリ](https://devdocs.magento.com/guides/v2.4/graphql/queries/customer-orders.html).

<pre>
<code class="language-graphql">
{
  customer {
    firstname
    lastname
    suffix
    email

    orders(filter:{number:{eq:"000000001"}}){
        items{
          billing_address {
firstname
lastname
street
city
region
region_id
postcode
telephone
country_code
}
shipping_address {
firstname
lastname
street
city
region
region_id
postcode
telephone
country_code
}
        }
    }
  }
}
</code>
</pre>

<u>期待される結果</u>:

ユーザーは注文情報を取得します。

<u>実際の結果</u>:

ユーザーに次のエラーが表示されます。 *&quot;message&quot;: &quot;内部サーバーエラー&quot;,*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
