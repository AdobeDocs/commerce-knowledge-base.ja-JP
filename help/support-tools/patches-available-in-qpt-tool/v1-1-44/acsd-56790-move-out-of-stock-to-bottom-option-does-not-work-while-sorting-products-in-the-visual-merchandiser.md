---
title: 'ACSD-56790: **[!UICONTROL move out of stock to bottom]で製品を並べ替えている場合、**のオプションは機能しません  [!DNL Visual Merchandiser]'
description: ACSD-56790 パッチを適用すると、ビジュアルマーチャンダイザーで商品を並べ替えている際に、「在庫切れを最下部に移動」オプションが機能しないAdobe Commerceの問題が修正されます。
feature: Products, Categories
role: Admin, Developer
exl-id: a0c61696-a12d-4c1a-a061-e2f17f38e1f4
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# ACSD-56790: **[!UICONTROL move out of stock to bottom]** で製品を並べ替えている場合、オプションが機能しない [!DNL Visual Merchandiser]

ACSD-56790 パッチは、で製品を並べ替えている際に、「在庫切れを最下部に移動」オプションが機能しない問題を修正しました。 [!DNL Visual Merchandiser]. このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.44 がインストールされています。 パッチ ID は ACSD-56790 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

この **[!UICONTROL move out of stock to bottom]** で製品を並べ替えている場合、オプションが機能しない [!DNL Visual Merchandiser]

<u>再現手順</u>:

1. Adobe Commerceをインストールします。
1. に移動 **[!UICONTROL Admin]** > **[!UICONTROL Stores]** > **[!UICONTROL Attributes]** > **[!UICONTROL Product]** 次の属性を作成します。
1. 新しい web サイトを作成します。 **非メイン**.
1. を作成 **非メインストア** この新しい web サイトで。
1. 2 つのストアを作成します。

   * の最初の **メイン Web サイト ストア**.
   * 次の中の 2 番目 **非メインストア**.

1. 2 つのソースを作成します。
   * レター。
   * 数値。

1. 2 つの在庫を作成します。
   * 最初のメイン – 販売チャネル：メイン web サイト – 割り当てられたソース：レター。
   * 2 番目の非メイン – 販売チャネル：非メイン – 割り当てソース：数値。

1. 両方の web サイトで 3 つのシンプルな製品を作成し、すべてをデフォルト カテゴリに、すべて両方のソースに割り当てます。

   * 製品 A – 数量 *10* レター内の数量 *0* を数字で表したもの。
   * 製品 1 – 数量 *0* レター内の数量 *10* を数字で表したもの。
   * 製品 A1 – 数量 *10* レター内の数量 *10* を数字で表したもの。

1. に移動 **[!UICONTROL Catalog]** > **[!UICONTROL Categories]** を選択して、  **[!UICONTROL Default category]**.
1. 範囲をに変更します。 **第 1**.
1. 「カテゴリ」セクションの製品を展開します。
1. 並べ替え順を次のように選択します。 **[!UICONTROL move out of stock to bottom]**

<u>期待される結果</u>:

を含む製品のリスト **在庫切れ** 製品が下部に移動されます。

<u>実際の結果</u>:

製品の読み込みに失敗する。 ページが管理者ダッシュボードにリダイレクトされ、次のエラーメッセージが表示されます。 `Invalid security or form key. Please refresh the page`

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
