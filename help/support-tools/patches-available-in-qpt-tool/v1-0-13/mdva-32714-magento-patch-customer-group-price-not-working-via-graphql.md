---
title: 「MDVA-32714 パッチ：お客様のグループ価格がGraphQLを介して機能しない」
description: MDVA-32714 パッチは、GraphQLの product query response でсustomer group price が追加されない問題を修正します。 このパッチは、Quality Patches Tool （QPT） 1.0.13 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。
exl-id: a4fc92ad-68dc-437d-8577-303007ef8a92
feature: GraphQL, Customer Service, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# MDVA-32714 パッチ：お客様のグループ価格がGraphQLで機能しない

>[!WARNING]
>
>MDVA-33975 という新しいパッチは、GraphQLの価格計算の問題を修正します。 MDVA-32714 は非推奨であり、パッチ MDVA-33975 を適用することをお勧めします。 このパッチにアクセスするには、サポートナレッジベースで [MDVA-33975 パッチ：GraphQL価格の計算 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/patches/mdva-33975-magento-patch-graphql-price-calculations.html) を参照してください。

MDVA-32714 パッチは、GraphQLの product query response でсustomer group price が追加されない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp)1.0.13 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.4 - 2.4.0-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

一般顧客の顧客グループ価格は、GraphQLの商品クエリ応答に追加されません。

<u> 再現手順 </u>:

1. 任意の顧客グループの任意の製品に対して特別価格を有効にして設定します。
1. GraphQLの商品クエリを使用してこの商品の価格を取得します。詳しくは、開発者向けドキュメントの [ 商品クエリ/サンプルクエリ ](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html#sample-queries) を参照してください。

<u> 期待される結果 </u>:

```api
price_range
```

管理パネルで定義された内容に応じて、一般顧客の割引価格を表示します。

<u> 実際の結果 </u>:

```api
price_range
```

一般顧客の割引価格は表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
