---
title: 「[!DNL ACSD-47280]：共有カタログを無効にすると間違った製品検索結果が表示される」
description: 共有カタログ機能が無効な場合に正しい検索結果が表示されるように、 [!DNL ACSD-47280] patch を適用して修正します。
exl-id: 98bbae42-fd68-4b54-823d-189d742cc35f
source-git-commit: 975f5b5c95ad488128a5dbb3488b8d54f7b73b59
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# [!DNL ACSD-47280]：共有カタログを無効にすると間違った製品検索結果が表示される

[!DNL ACSD-47280] パッチは、[!DNL shared catalog] 機能が無効な場合の正しい検索結果の表示を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.22 がインストールされている場合に使用できます。 [!DNL patch ID] は [!DNL ACSD-47280] です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 [!DNL patch ID] を検索キーワードとして使用して、パッチを見つけます。

## 問題

[!DNL shared catalog] を無効にすると、誤った製品検索結果が表示される。

<u> 前提条件 </u>:

* [!DNL B2B] モジュールがインストールされました

<u> 再現手順 </u>:

1. 2 番目の web サイトを作成します。
1. 2 つ目の web サイトに製品を割り当てます。
1. **2 番目の web サイト** で次の [!DNL GraphQL] を使用して製品を確認します。

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

1. デフォルト [!DNL scope] で **[!UICONTROL Shared Catalog]** を有効にします。
1. [!DNL GraphQL] のリクエストで、2 番目の web サイトの製品が表示されなくなりました。これは正しい結果です。
1. 2 つ目の web サイトの [!DNL scope] に移動し、**[!UICONTROL Company]** を無効にします。

<u> 期待される結果 </u>:

[!DNL GraphQL] のリクエストでは、2 番目の web サイトの製品が引き続き表示されます。

<u> 実際の結果 </u>:

[!DNL GraphQL] のリクエストでは、2 番目の web サイトの製品は表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
