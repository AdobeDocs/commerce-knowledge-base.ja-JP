---
title: '"ACSD-55100: [!DNL GraphQL] 検索結果で 10,000 個を超える製品が返されない」'
description: ACSD-55100 パッチを適用すると、GraphQLが検索結果で*10k*を超える商品を返さないAdobe Commerceの問題を修正できます。
feature: GraphQL, Products, Search
role: Admin, Developer
exl-id: 951e5cd4-9690-43df-9e51-deab73f9eb54
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# ACSD-55100: [!DNL GraphQL] 検索結果で 10,000 個を超える製品が返されない

ACSD-55100 パッチは、次の問題を修正します。 [!DNL GraphQL] 次の値を超える製品は返さない *10k* を検索結果で使用できます。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.46 がインストールされています。 パッチ ID は ACSD-55100 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

[!DNL GraphQL] 次の値を超える製品は返さない *10k* を検索結果で使用できます。

<u>前提条件</u>:

の場合 **[!DNL OpenSearch]**&#x200B;使用可能な最新バージョンを使用していることを確認してください。

報告された問題を解決するために、ポイントインタイム機能が導入されました（後で利用可能になります） **[!DNL OpenSearch]** 2.5.0。のバージョン 2.2 が必要 `opensearch-project/opensearch-php` パッケージ。

ただし、と競合しています `magento/magento-cloud-metapackage`。に対する依存関係を指定します。 `opensearch-project/opensearch-php` バージョン 2.0.1 未満である必要があるパッケージ。


この依存関係により、 [opensearch-project/opensearch-php] 最新バージョン 2.2 にパッケージ化します。

その結果、次のエラーが発生し、を超える製品については null 結果が返されます *10,000*.

`Namespace [createPointInTime] not found in /vendor/opensearch-project/opensearch-php/src/OpenSearch/Client.php:135`

既存の依存関係があると、にバージョンを直接追加するのが難しくなります `composer.json` をファイルに保存して更新します `opensearch-project/opensearch-php` バージョン 2.2 にパッケージ化します。

この問題を解決するには、メインに次の行を含めます `composer.json` ファイルは必須ブロックの下にあります。 その後、を再デプロイして、問題のあるパッケージを最新バージョンに更新します。

`"opensearch-project/opensearch-php": "2.2.0 as 2.0.0",`

<u>再現手順</u>:

1. を使用したカタログの生成 *15k* 製品。
1. を送信 [!DNL GraphQL]:

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

<u>期待される結果</u>:

Total_count = *15k*
すべての製品を表示できるはずです。

<u>実際の結果</u>:

Total_count = *10k*
これ以上これ以上表示する商品を取得することはできません *10k* バッチ。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
