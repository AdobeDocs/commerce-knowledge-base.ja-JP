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

ACSD-51120 パッチでは、ステージングアップデートによって更新された CMS ブロックを含む CMS ページのGraphQL GETリクエストキャッシュがクリアされない問題が修正されています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.33 がインストールされている場合に使用できます。 パッチ ID は ACSD-51120 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.2-p2

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ステージングアップデートにより更新された CMS ブロックを含む CMS ページのGraphQL GETリクエストキャッシュがクリアされない。

<u> 再現手順 </u>:

1. CMS ブロックを作成します。
1. [!DNL Page Builder] を使用して、CMS ブロックを CMS ページに含めます。
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

1. GraphQLの応答が [!DNL Varnish] にキャッシュされていることを確認します。
1. ブロックに対してスケジュールされた更新を作成します。
1. スケジュールされた更新が適用されるのを待ってから、cron ジョブを実行してスケジュールされた更新を適用します。
1. GETリクエストを使用して指定されたGraphQL クエリを使用して CMS ページを再度取得します。

<u> 期待される結果 </u>:

応答には、更新されたコンテンツが表示されます。

<u> 実際の結果 </u>:

応答には古いコンテンツが引き続き表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。


## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
