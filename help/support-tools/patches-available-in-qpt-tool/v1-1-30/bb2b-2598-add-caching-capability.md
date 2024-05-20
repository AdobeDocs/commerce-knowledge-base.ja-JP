---
title: 「BB2B-2598:storeConfig、通貨、国、国、availableStores GraphQl クエリにキャッシュ機能を追加」
description: BB2B-2598 パッチを適用して、storeConfig、currency、country、countries、および availableStores の各 GraphQl クエリにキャッシュ機能を追加します。
exl-id: 37551954-d721-4f3a-b237-cd795f715a5f
feature: B2B, GraphQL, Cache
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# BB2B-2598：にキャッシュ機能を追加 `storeConfig`, `currency`, `country`, `countries`、および `availableStores` GraphQl クエリ

BB2B-2598 パッチは、次のキャッシュ機能を追加します。 `storeConfig`, `currency`, `country`, `countries`、および `availableStores` GraphQl クエリ このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.30 がインストールされています。 パッチ ID は BB2B-2598 です。 この問題はAdobe Commerce 2.4.7-beta1 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

`availableStores`, `countries`, `country`, `currency`, `storeConfig`、および `customAttributeMetadata` GraphQL クエリはキャッシュできません。

<u>前提条件</u>:

* サーバーが次を指している [!DNL Varnish] Adobe Commerce バックエンドへのプロキシ化。
* 設定 `system/full_page_cache/caching_application` はに設定されています。 *2* （[!DNL Varnish]）、または、Adobe Commerce管理者/に移動します。 **[!UICONTROL Stores]** > **[!UICONTROL System]** > **[!UICONTROL Full Page Cache]** > **[!UICONTROL Caching Application]** > に設定し、に設定します [!DNL Varnish].

パッチを適用した後、次の手順を実行して、キャッシュ機能が使用可能になっていることを確認します。

1. 送信 `GET` 任意のフィールドを使用して、上記のGraphQL クエリのいずれかにリクエストします。
1. 変更を加えずにリクエストを再送信します。ずっと速くなっていることがわかります。 リクエストはバックエンドに送信されませんが、によって完全に処理されます。 [!DNL Varnish] キャッシュヒットとして。
1. さらにプルーフが必要な場合は、未設定をコメントアウトします。 `X-Magento-Debug` ヘッダーがに存在する [VCL](https://github.com/magento/magento2/blob/026e5b29a5edfd619bbdea62d636b3cab2ea03b4/app/code/Magento/PageCache/etc/varnish6.vcl#L227)を選択してから、再起動します [!DNL Varnish] そして、上記の手順を再度実行します。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
