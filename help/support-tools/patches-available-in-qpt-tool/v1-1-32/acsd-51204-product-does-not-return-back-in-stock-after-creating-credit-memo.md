---
title: 「ACSD-51204：商品がクレジットメモの作成後に在庫として返されない」
description: ACSD-51204 パッチを適用すると、クレジットメモを作成した後、商品が在庫に戻らないAdobe Commerceの問題を修正できます。
feature: Orders, Products, Returns
role: Admin
exl-id: 302033bc-2ca5-40d6-b692-24ae46b21c31
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# ACSD-51204：クレジットメモを作成した後、商品が在庫に戻らない

ACSD-51204 パッチは、クレジットメモを作成した後、製品が在庫に戻らない問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.32 がインストールされている場合に使用できます。 パッチ ID は ACSD-51204 です。 この問題はAdobe Commerce 2.4.7 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.6-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

売り切れた商品は、クレジットメモを作成した後、在庫として返されません。

<u> 再現手順 </u>:

1. **[!UICONTROL Adobe Commerce]** をインストールし、デフォルトの *source* および *stock* のみで **[!UICONTROL Inventory Management Module]** を有効にします。
1. 量が *10* の **[!UICONTROL new product]** を追加します。
1. 製品を **[!UICONTROL default stock]** に割り当てます。
1. ストアフロントで、商品をカートに追加し、利用可能な全数量 10 を注文します。
1. 管理パネルで、注文の *請求書* および *出荷* を生成します。
1. すべての項目に対して「*在庫に戻る* チェックボックスが選択された **[!UICONTROL Credit Memo]** ージを作成します。
1. 管理者で製品の **[!UICONTROL Salable Quantity]** を確認します。

<u> 期待される結果 </u>:

商品の販売可能数量は *10* に戻る必要があります。

<u> 実際の結果 </u>:

販売可能数量は *0* のままです。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html>) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>)」を参照してください。
