---
title: 'ACSD-48234：次の場合に、カタログ検索結果のカテゴリ項目数が正しくない [!UICONTROL Display Out of Stock Products] 有効'
description: 次の場合に、カタログ検索結果に誤ったカテゴリ項目数が表示されるAdobe Commerceの問題を修正するために、ACSD-48234 パッチを適用してください [!UICONTROL Display Out of Stock Products] 」オプションが有効になっています。
exl-id: 8e70fe73-d550-4e11-b25e-84955e136d12
feature: Admin Workspace, Categories, Catalog Management, Orders, Products, Search
role: Admin
source-git-commit: 3eeb86c2644f8a04ddcf5e205bc400d2ca9969af
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# ACSD-48234：カタログ検索結果に誤ったカテゴリ項目数が表示される **[!UICONTROL Display Out of Stock Products]** enabled

ACSD-48234 パッチは、次の場合にカタログ検索結果に誤ったカテゴリ項目数が表示される問題を解決します **[!UICONTROL Display Out of Stock Products]** 」オプションが有効になっています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.25 がインストールされています。 パッチ ID は ACSD-48234 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。


## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.5-p4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

次の場合、カタログ検索結果に誤ったカテゴリ項目数が表示される **[!UICONTROL Display Out of Stock Products]** 」オプションが有効になっています。

<u>再現手順</u>:

1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Attributes]** > **[!UICONTROL Product]** を開きます。 **[!UICONTROL color]** 属性。
1. オレンジと緑など、2 つのオプションを追加します。 属性を保存します。
1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Attributes]** > **[!UICONTROL Attribute Set]** を追加して、 **[!UICONTROL color]** の属性 **[!UICONTROL Default]** 属性セット。
1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL CATALOG]** > **[!UICONTROL Inventory]** > **[!UICONTROL Stock Options]** およびを設定 **[!UICONTROL Display Out of Stock Products]** 対象： _はい_.
1. カテゴリ「cat1」を作成します。
1. 2 つの製品を作成します。
   1. 名前：prod1、色：オレンジ、カテゴリ：cat1。
   1. 名前：prod2、色：緑、カテゴリ：cat1。
1. ストアフロントの cat1 カテゴリを開きます。
1. レイヤ ナビゲーションでオレンジ色を選択します。

<u>期待される結果</u>:

prod1 製品のみが表示されます。

<u>実際の結果</u>:

prod1 製品と prod2 製品の両方が表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
