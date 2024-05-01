---
title: 「ACSD-51120:CMS ブロックを含む CMS ページのGraphQL GETリクエストキャッシュがクリアされない」
description: ACSD-51120 パッチを適用すると、CMS ブロックを含んだ CMS ページのGraphQL GETリクエストキャッシュがクリアされないAdobe Commerceの問題が修正されます。
exl-id: 22abba89-b697-45d7-972e-bf3233e5e9ec
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# ACSD-51120:CMS ブロックを含む CMS ページのGraphQL GETリクエストキャッシュがクリアされない

ACSD-51120 パッチでは、ステージングアップデートによって更新された CMS ブロックを含む CMS ページのGraphQL GETリクエストキャッシュがクリアされない問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.33 がインストールされています。 パッチ ID は ACSD-51120 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.2-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ステージングアップデートにより更新された CMS ブロックを含む CMS ページのGraphQL GETリクエストキャッシュがクリアされない。

<u>再現手順</u>:

1. CMS ブロックを作成します。
1. を使用して、CMS ブロックを CMS ページに含める [!DNL Page Builder].
1. GETリクエストを使用して、指定されたGraphQL クエリを使用して CMS ページを取得します。

   ```GraphQL
   {
   cmsPage( identifier: "<CMS PAGE IDENTIFIER>") {
       content
       content_heading
       identifier
       meta_description
       meta_keywords
       meta_title
       page_layout
       title
       url_key
   }
   }
   ```

1. GraphQLの応答がにキャッシュされていることを確認します。 [!DNL Varnish].
1. ブロックに対してスケジュールされた更新を作成します。
1. スケジュールされた更新が適用されるのを待ってから、cron ジョブを実行してスケジュールされた更新を適用します。
1. GETリクエストを使用して指定されたGraphQL クエリを使用して CMS ページを再度取得します。

<u>期待される結果</u>:

応答には、更新されたコンテンツが表示されます。

<u>実際の結果</u>:

応答には古いコンテンツが引き続き表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。


## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
