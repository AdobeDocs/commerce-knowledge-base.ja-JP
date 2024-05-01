---
title: '''ACSD-56193: [!DNL Fastly] コンテンツのステージング更新のキャッシュがクリアされません'
description: Adobe Commerce ACSD-56193 パッチを適用して、 [!DNL Fastly] コンテンツのステージング更新でキャッシュがクリアされない。
feature: Cache, GraphQL, Staging
role: Admin, Developer
exl-id: d4bbfafa-2d24-44cf-a08b-f7dd9111a65b
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# ACSD-56193: [!DNL Fastly] コンテンツのステージング更新でキャッシュがクリアされない

ACSD-56193 パッチは、 [!DNL Fastly] コンテンツのステージング更新でキャッシュがクリアされない。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.44 がインストールされています。 パッチ ID は ACSD-56193 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

この [!DNL Fastly/Varnish] コンテンツのステージング更新でキャッシュがクリアされない

<u>再現手順</u>:

1. インストールと設定 [!DNL Varnish] キャッシュ。
1. スケジュールされた更新で静的ブロックを作成します。
1. 静的ブロックを埋め込むカテゴリを作成します。
1. 以下のGraphQL クエリを使用して、カテゴリのコンテンツを取得します。

   ```GraphQL
      query GetCategories($id: String!) {
         categoryList(filters: { category_uid: { eq: $id } }) 
       {
           meta_title
           meta_keywords
           meta_description
           description
           path
           cms_block {
             content
             identifier
             title
             __typename
           }
           __typename
       }
     }
     {"id":"Mwo="}
   ```

1. このクエリを複数回実行し、応答がにキャッシュされていることを確認します [!DNL Varnish].
1. cron を実行して、スケジュールされた変更を適用します。
1. 上記のGraphQL クエリを再度実行します。
1. 同じ静的ブロックに対して新しいスケジュールを作成します。
1. 5～9 の手順を繰り返します。

<u>期待される結果</u>:

スケジュールされた更新の実行後、更新されたコンテンツが返されます。

<u>実際の結果</u>:

スケジュールされた更新が実行されると、古いコンテンツが返されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
