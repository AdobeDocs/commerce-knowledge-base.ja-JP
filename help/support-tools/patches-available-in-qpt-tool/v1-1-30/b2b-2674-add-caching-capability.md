---
title: 「B2B-2674:customAttributeMetadata GraphQL クエリにキャッシュ機能を追加します」
description: B2B-2674 パッチを適用して、customAttributeMetadata GraphQL クエリにキャッシュ機能を追加します。
feature: Attributes, B2B, Cache, GraphQL
role: Admin
exl-id: a4efb268-f811-41f2-a788-a8cfc3016f61
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# B2B-2674: キャッシュ機能をに追加します `customAttributeMetadata` GraphQL クエリ

B2B-2674 パッチは、 `customAttributeMetadata` GraphQL クエリ。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.30 がインストールされています。 パッチ ID は B2B-2674 です。 この問題はAdobe Commerce 2.4.7-beta1 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

`customAttributeMetadata` GraphQL クエリはキャッシュできません。

<u>前提条件</u>:

* サーバーが次を指している [!DNL Varnish] Adobe Commerce バックエンドへのプロキシ化。
* 設定 `system/full_page_cache/caching_application` はに設定されています。 *2* （[!DNL Varnish]）、または、Adobe Commerce管理者/に移動します。 **[!UICONTROL Stores]** > **[!UICONTROL System]** > **[!UICONTROL Full Page Cache]** > **[!UICONTROL Caching Application]** > に設定し、に設定します [!DNL Varnish].

パッチを適用した後、次の手順を実行して、キャッシュ機能が使用可能になっていることを確認します。

1. 送信 `GET` 任意のフィールドを使用して、上記のGraphQL クエリにリクエストします。
1. 変更を加えずにリクエストを再送信します。ずっと速くなっていることがわかります。 リクエストはバックエンドに送信されませんが、によって完全に処理されます。 [!DNL Varnish] キャッシュヒットとして。
1. さらにプルーフが必要な場合は、未設定をコメントアウトします。 `X-Magento-Debug` ヘッダーがに存在する [VCL](https://github.com/magento/magento2/blob/2.4-develop/app/code/Magento/PageCache/etc/varnish6.vcl#L239)を選択してから、再起動します [!DNL Varnish] そして、上記の手順を再度実行します。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
