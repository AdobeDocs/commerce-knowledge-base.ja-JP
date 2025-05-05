---
title: 「ACSD-49042：順不同の商品はストアフロントから注文できない」
description: ACSD-49042 パッチを適用すると、順不同の商品をストアフロントから注文できないAdobe Commerceの問題を修正できます。
exl-id: b9227296-f300-447c-a241-30ccc0691c9a
feature: Admin Workspace, Orders, Products, Storefront
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# ACSD-49042：順不同の商品はストアフロントからは注文できません

ACSD-49042 パッチでは、順不同の商品をストアフロントから注文できない問題を修正しました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.27 がインストールされている場合に使用できます。 パッチ ID は ACSD-49042 です。 この問題はAdobe Commerce 2.4.5 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.4-p2

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

このエラーは、順不同の商品をストアフロントから注文できない場合に発生します。

<u> 再現手順 </u>:

1. 次の設定を行います。
   * **[!UICONTROL Display Out of Stock Products]** を *[!UICONTROL Yes]* に設定します。
   * **[!UICONTROL Backorders]** を *[!UICONTROL Allow Qty Below 0]* に設定します。
1. 新しい **[!DNL custom stock]** と **[!DNL custom source]** を追加します。
1. **[!DNL custom source]** に製品を割り当て、その製品の在庫番号が設定されていることを確認してください（例：*10*）。
1. 製品の編集ページで、**[!UICONTROL Advanced Inventory]** を開きます。 カートに **[!UICONTROL minimum quantity]** を設定します（例：*160*）。 数量は在庫より上である必要があります。
1. 店頭に移動し、商品を購入して予約を作成します。
1. **[!UICONTROL product quantity]** を *0* に変更します。 重要なポイントは、予約がある場合に **[!DNL Admin panel]** から製品を保存することです。
1. ストアフロントで **[!UICONTROL product page]** を開き、商品をカートに追加してみてください。

<u> 期待される結果 </u>:

*0* 未満の数量のバックオーダーは許可されているので、買い物かごに製品を追加できます。

<u> 実際の結果 </u>:

商品が在庫切れと表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
