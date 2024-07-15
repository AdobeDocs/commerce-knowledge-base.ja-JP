---
title: '「ACSD-55100: [!DNL GraphQL] 10k を超える製品は検索結果に返されない」'
description: ACSD-55100 パッチを適用すると、GraphQLが検索結果で*10k*を超える商品を返さないAdobe Commerceの問題を修正できます。
feature: GraphQL, Products, Search
role: Admin, Developer
exl-id: 951e5cd4-9690-43df-9e51-deab73f9eb54
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# ACSD-55100：検索結果で [!DNL GraphQL] が 10,000 個を超える製品を返さない

ACSD-55100 パッチは、検索結果で *10k* を超える製品が [!DNL GraphQL] に返されない問題を修正しました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.46 がインストールされている場合に使用できます。 パッチ ID は ACSD-55100 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

[!DNL GraphQL] は、検索結果で *10k* を超える製品は返しません。

<u> 前提条件 </u>:

**[!DNL OpenSearch]** の場合は、利用可能な最新バージョンを使用していることを確認してください。

報告された問題を解決するために、ポイントインタイム機能が導入されました。この機能は **[!DNL OpenSearch]** 2.5.0 以降で使用でき、`opensearch-project/opensearch-php` パッケージのバージョン 2.2 が必要です。

ただし、`magento/magento-cloud-metapackage` との競合があり、`opensearch-project/opensearch-php` パッケージへの依存関係が指定されているので、バージョン 2.0.1 未満にする必要があります。


この依存関係により、[opensearch-project/opensearch-php] パッケージを最新バージョン 2.2 に更新できなくなります。

その結果、次のエラーが発生し、*10,000* を超える製品に対して null 結果が返されます。

`Namespace [createPointInTime] not found in /vendor/opensearch-project/opensearch-php/src/OpenSearch/Client.php:135`

既存の依存関係があると、`composer.json` ファイルにバージョンを直接追加して、`opensearch-project/opensearch-php` パッケージをバージョン 2.2 にアップデートすることが難しくなります。

この問題を解決するには、メインの `composer.json` ファイルの require ブロックに次の行を追加します。 その後、を再デプロイして、問題のあるパッケージを最新バージョンに更新します。

`"opensearch-project/opensearch-php": "2.2.0 as 2.0.0",`

<u> 再現手順 </u>:

1. *15k* 製品のカタログを生成します。
1. [!DNL GraphQL] を送信します。

```
    query {
    products(
    filter: {
    # category_id:{eq:""}
    }
    , pageSize: 5, currentPage: 1

    ) {
    total_count
    page_info {
    current_page
    page_size
    total_pages
     }

     aggregations {

    attribute_code
    count
    label
    options {
    label
    value

    }
    }

    items {
    uid
    sku
    is_for_clearance
    categories {
    name
    breadcrumbs {
    category_name
    category_uid
    }
    display_mode
    description
    }
    }
    }
    }
```

<u> 期待される結果 </u>:

Total_count = *15k*
すべての製品を表示できるはずです。

<u> 実際の結果 </u>:

Total_count = *10k*
*10k* バッチの後に表示する製品はこれ以上取得できません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
