---
title: 「ACSD-52801:GraphQL製品フィルタークエリに部分一致の結果が表示されない」
description: ACSD-52801 パッチを適用すると、GraphQL製品フィルタークエリに部分一致の結果が表示されないAdobe Commerceの問題が修正されます。
feature: Products
role: Admin, Developer
exl-id: a03a4d09-ebec-4ad0-a875-48e000a29b44
source-git-commit: 40968db03939058884bca4e4aeed2ffef0462e0b
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# ACSD-52801:GraphQL製品フィルタークエリに部分一致の結果が表示されない

ACSD-52801 パッチでは、GraphQLの製品フィルタークエリに部分一致の結果が表示されない問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.40 がインストールされています。 パッチ ID は ACSD-52801 です。 この問題はAdobe Commerce 2.4.7 で修正されていることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p2、2.4.5-p4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

GraphQL製品フィルタークエリに部分一致の結果が表示されません。

<u>再現手順</u>:

1. サンプルデータを含んだクリーンなインスタンスをインストールします。
1. 次のGraphQL クエリを実行します。

```GraphQL
{
  products(
    filter: { name: { match: "Life" } }
    sort: { position: ASC }
    pageSize: 100
    currentPage: 1
  ) {
    total_count
    items {
      url_key
      sku
      name
      meta_title
    }
  }
}
```

<u>期待される結果</u>:

を追加することで、ストアフロントの事前検索と同様の一致結果が可能になります。 `match_type` （[!UICONTROL PARTIAL], [!UICONTROL FULL]）属性を使用して必要な結果を制御します。 [!UICONTROL FULL] 完全な単語に一致し、 [!UICONTROL PARTIAL] 生涯に含まれる人生のような部分的な単語に一致します。

<u>実際の結果</u>:

製品フィルタークエリは、検索キーワードの部分一致の結果を返しません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
