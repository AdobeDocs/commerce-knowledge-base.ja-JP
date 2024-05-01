---
title: 「ACSD-51792：ページにインプレッションイベントがない」
description: Google Tag Manager 4 が有効になっているときにページにインプレッションイベントが発生しないAdobe Commerceのパフォーマンスの問題を修正するため、ACSD-51792 パッチを適用してください。
exl-id: 59194d4c-c387-4372-a0ff-1cdd74f8c6df
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# ACSD-51792：ページにインプレッションイベントがありません

ACSD-51792 パッチは、次の場合にページにインプレッションイベントが含まれないパフォーマンスの問題を修正します [!DNL Google Tag Manager] 4 が有効になっています。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.33 がインストールされています。 パッチ ID は ACSD-51792 です。 この問題はAdobe Commerce 2.4.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.5-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

次の場合、ページにはインプレッションイベントがありません [!DNL Google Tag Manager] 4 が有効になっています。

<u>再現手順</u>:

1. に移動 **[!UICONTROL Admin]** > **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** > **[!UICONTROL Google API]**.
1. の設定 **[!DNL GoogleTag Manager]** 統合。
1. に移動 [Google Tag Assistant](https://tagassistant.google.com/)を開き、web サイトへの接続に必要な手順を完了します。
1. ストアフロントに製品リストが表示されているカテゴリページを開きます。
1. Tag Assistant オブザーバーでインプレッションイベントを確認します。

<u>期待される結果</u>:

インプレッションイベントは、ページ上のすべての製品から始める必要があります。

<u>実際の結果</u>:

ページには、タグアシスタントオブザーバー内のインプレッションイベントがありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
