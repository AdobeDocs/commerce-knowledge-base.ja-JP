---
title: 「ACSD-55231：クイックオーダー機能の使用中に SKU が見つからないというエラー」
description: ACSD-55231 パッチを適用すると、クイックオーダー機能を使用して買い物かごに商品を追加しようとすると、「The SKU was not found in the catalog」（SKU がカタログに見つかりませんでした）というエラーが発生するAdobe Commerceの問題を修正できます。
feature: Products, Checkout, B2B
role: Admin, Developer
exl-id: 463c2c07-39ec-4b03-81f7-ec2f71f5af76
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# ACSD-55231：クイックオーダー機能の使用中に SKU が見つからないというエラーが発生する

ACSD-55231 パッチは、発生した問題を修正します *「カタログに SKU が見つかりませんでした」* クイックオーダー機能を使用して買い物かごに製品を追加しようとするとエラーが発生する。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.44 がインストールされています。 パッチ ID は ACSD-55231 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

取得 *「カタログに SKU が見つかりませんでした」* クイックオーダー機能を使用して買い物かごに追加する製品を検索中にエラーが発生します。

<u>再現手順</u>:

1. B2B モジュールと共にAdobe Commerceをインストールします。
1. に移動します。 **[!UICONTROL Admin]** > **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL B2B Features]** さらに、次のように設定します。
   * **[!UICONTROL Enable company]**: *はい*
   * **[!UICONTROL Enable Shared Catalog]**: *はい*
   * **[!UICONTROL Enable Quick Order]**: *はい*
1. 上記の設定を保存します。
1. に移動 **[!UICONTROL Catalog]** > **[!UICONTROL Shared Catalogs]** 新しい共有カタログを作成します。
1. に移動します。 **[!UICONTROL Customers]** > **[!UICONTROL All Customers]** 新しい顧客を作成します。
   * グループ フィールドで、最近作成した共有カタログを選択し、 *[!UICONTROL Allow remote shopping assistance]* 対象： *はい*.
1. SKU を使用したシンプルな製品の生成 *p12*、カテゴリに関連付けます *c1*&#x200B;を開き、で新しく作成した共有カタログを選択します。 [!UICONTROL Product in Shared Catalog] セクション。
1. 実行：

   ```
   bin/magento ind:rei 
   bin/magento c:f 
   bin/magento cron:run (multiple times)
   ```

1. 管理ページを更新します。
1. に移動します。 **[!UICONTROL Customers]** > **[!UICONTROL All Customers]** および前に作成した顧客を編集します。
1. クリック **[!UICONTROL Login as customer]**.
1. に移動 **[!UICONTROL Quick order]**.
1. を検索 *p12* SKU を選択し、 **[!UICONTROL Product Suggestion]**.
1. この商品を買い物かごに追加して注文します。
1. に戻る **[!UICONTROL Quick Order]**、SKU を検索 *p12* 再度クリックして、 **[!UICONTROL Product Suggestion]**.

<u>期待される結果</u>:

クイックオーダー機能を使用して、商品を買い物かごに追加できます。

<u>実際の結果</u>:

クイックオーダー機能を使用して買い物かごに製品を追加して次を取得することはできません *「カタログに SKU が見つかりませんでした」* 製品 SKU の検索中にエラーが発生しました。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
