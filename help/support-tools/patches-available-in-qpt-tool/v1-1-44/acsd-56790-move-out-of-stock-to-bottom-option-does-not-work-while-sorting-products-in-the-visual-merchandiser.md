---
title: 「ACSD-56790:**[!UICONTROL move out of stock to bottom]**オプションが、 [!DNL Visual Merchandiser] 内の製品の並べ替え中に機能しない」
description: ACSD-56790 パッチを適用すると、ビジュアルマーチャンダイザーで商品を並べ替えている際に、「在庫切れを最下部に移動」オプションが機能しないAdobe Commerceの問題が修正されます。
feature: Products, Categories
role: Admin, Developer
exl-id: a0c61696-a12d-4c1a-a061-e2f17f38e1f4
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# ACSD-56790:[!DNL Visual Merchandiser] 内の製品の並べ替え中に、**[!UICONTROL move out of stock to bottom]** のオプションが機能しない

ACSD-56790 パッチでは、[!DNL Visual Merchandiser] ージ内の製品を並べ替える際に、「在庫切れを最下部に移動」オプションが機能しない問題を修正しています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.44 がインストールされている場合に使用できます。 パッチ ID は ACSD-56790 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

[!DNL Visual Merchandiser] 内の製品の並べ替え中に「**[!UICONTROL move out of stock to bottom]**」オプションが機能しない

<u> 再現手順 </u>:

1. Adobe Commerceをインストールします。
1. **[!UICONTROL Admin]**/**[!UICONTROL Stores]**/**[!UICONTROL Attributes]**/**[!UICONTROL Product]** に移動し、次の属性を作成します。
1. 新しい web サイト **Non-main** を作成します。
1. この新しい web サイトに **非メインストア** を作成します。
1. 2 つのストアを作成します。

   * 最初に **メイン web サイトストア**。
   * 次に **非メインストア** です。

1. 2 つのソースを作成します。
   * レター。
   * 数値。

1. 2 つの在庫を作成します。
   * 最初のメイン – 販売チャネル：メイン web サイト – 割り当てられたソース：レター。
   * 2 番目の非メイン – 販売チャネル：非メイン – 割り当てソース：数値。

1. 両方の web サイトで 3 つのシンプルな製品を作成し、すべてをデフォルト カテゴリに、すべて両方のソースに割り当てます。

   * ProductA – 数量 *10* （文字）、数量 *0* （数字）。
   * Product1 - レターの数量 *0*、数値の数量 *10*。
   * ProductA1 - レターの数量 *10*、数値の数量 *10*。

1. **[!UICONTROL Catalog]**/**[!UICONTROL Categories]** に移動し、「**[!UICONTROL Default category]**」を選択します。
1. 範囲を **最初** に変更します。
1. 「カテゴリ」セクションの製品を展開します。
1. 並べ替え順を次のように選択します。**[!UICONTROL move out of stock to bottom]**

<u> 期待される結果 </u>:

**在庫切れ** の商品のリストが下部に移動します。

<u> 実際の結果 </u>:

製品の読み込みに失敗する。 ページが管理者ダッシュボードにリダイレクトされ、次のエラーメッセージが表示されます。`Invalid security or form key. Please refresh the page`

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
