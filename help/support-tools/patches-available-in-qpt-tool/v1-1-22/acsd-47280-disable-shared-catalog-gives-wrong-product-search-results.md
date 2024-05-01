---
title: '''[!DNL ACSD-47280]「共有カタログを無効にすると間違った製品検索結果が表示される」'
description: を適用 [!DNL ACSD-47280] 共有カタログ機能が無効な場合に、正しい検索結果が表示されるように修正するパッチ。
exl-id: 98bbae42-fd68-4b54-823d-189d742cc35f
source-git-commit: 975f5b5c95ad488128a5dbb3488b8d54f7b73b59
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# [!DNL ACSD-47280]：共有カタログを無効にすると、間違った製品検索結果が表示される

この [!DNL ACSD-47280] patch は、 [!DNL shared catalog] この機能は無効です。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.22 がインストールされています。 この [!DNL patch ID] 等しい [!DNL ACSD-47280]. この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). の使用 [!DNL patch ID] 検索キーワードとして使用して、パッチを見つけます。

## 問題

無効化 [!DNL shared catalog] が間違った製品検索結果を表示する。

<u>前提条件</u>:

* [!DNL B2B] インストールされているモジュール

<u>再現手順</u>:

1. 2 番目の web サイトを作成します。
1. 2 つ目の web サイトに製品を割り当てます。
1. 製品の確認 **第 2 の web サイト** 使用 [!DNL GraphQL]:

   ```GraphQL
   {
     products(search: "bag", pageSize: 2) {
       total_count
       items {
         name
         sku
       }
       page_info {
         page_size
         current_page
       }
     }
   }
   ```

1. Enable （有効） **[!UICONTROL Shared Catalog]** デフォルト [!DNL scope].
1. この [!DNL GraphQL] リクエストで 2 番目の web サイトの製品が表示されなくなりました。これは正しい結果です。
1. に移動します [!DNL scope] （2 番目の web サイトおよび無効化） **[!UICONTROL Company]**.

<u>期待される結果</u>:

この [!DNL GraphQL] リクエストで 2 番目の web サイトの製品が引き続き表示されます。

<u>実際の結果</u>:

この [!DNL GraphQL] リクエストで、2 番目の web サイトの製品が表示されない。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
