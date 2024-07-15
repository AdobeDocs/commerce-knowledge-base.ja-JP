---
title: 「BB2B-2598:storeConfig、通貨、国、国、availableStores GraphQl クエリにキャッシュ機能を追加」
description: BB2B-2598 パッチを適用して、storeConfig、currency、country、countries、および availableStores の各 GraphQl クエリにキャッシュ機能を追加します。
exl-id: 37551954-d721-4f3a-b237-cd795f715a5f
feature: B2B, GraphQL, Cache
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# BB2B-2598:`storeConfig`、`currency`、`country`、`countries` および `availableStores` GraphQl クエリにキャッシュ機能を追加します

BB2B-2598 パッチは、`storeConfig`、`currency`、`country`、`countries`、および `availableStores` GraphQl クエリにキャッシュ機能を追加します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.30 がインストールされている場合に使用できます。 パッチ ID は BB2B-2598 です。 この問題はAdobe Commerce 2.4.7-beta1 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

`availableStores`、`countries`、`country`、`currency`、`storeConfig` および `customAttributeMetadata` GraphQLの各クエリはキャッシュできません。

<u> 前提条件 </u>:

* サーバーは、Adobe Commerce バックエンドへ [!DNL Varnish] プロキシを指しています。
* 構成設定 `system/full_page_cache/caching_application` が *2* （[!DNL Varnish]）に設定されているか、Adobe Commerce管理/**[!UICONTROL Stores]**/**[!UICONTROL System]**/**[!UICONTROL Full Page Cache]**/**[!UICONTROL Caching Application]** に移動して、[!DNL Varnish] に設定してください。

パッチを適用した後、次の手順を実行して、キャッシュ機能が使用可能になっていることを確認します。

1. 任意 `GET` フィールドを使用して、上記のGraphQL クエリのいずれかにリクエストを送信します。
1. 変更を加えずにリクエストを再送信します。ずっと速くなっていることがわかります。 リクエストはバックエンドに送信されませんが、キャッシュヒットとして [!DNL Varnish] で完全に処理されます。
1. さらにプルーフが必要な場合は、[VCL](https://github.com/magento/magento2/blob/026e5b29a5edfd619bbdea62d636b3cab2ea03b4/app/code/Magento/PageCache/etc/varnish6.vcl#L227) に存在する `X-Magento-Debug` ヘッダーの未設定をコメントアウトし、[!DNL Varnish] を再起動して、上記の手順を再実行します。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
