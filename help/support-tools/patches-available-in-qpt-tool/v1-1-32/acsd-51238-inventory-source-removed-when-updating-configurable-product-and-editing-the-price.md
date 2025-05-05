---
title: 「ACSD-51238：設定可能な製品を更新して価格を編集すると、在庫ソースが削除される」
description: 設定可能な商品をアップデートして価格を編集する際に、在庫ソースが削除されるAdobe Commerceの問題を修正するために、ACSD-51238 パッチを適用してください。
exl-id: ab2f60fd-5da3-45f7-a489-6f4f9d34e1f1
feature: Configuration, Inventory, Orders, Products
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# ACSD-51238：設定可能な製品を更新して価格を編集すると、在庫ソースが削除される

ACSD-51238 パッチは、設定可能な製品を更新して価格を編集する際に在庫ソースが削除される問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.32 がインストールされている場合に使用できます。 パッチ ID は ACSD-51238 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja>) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

設定可能な商品を更新し、価格を編集すると、在庫ソースが削除されます。

<u> 再現手順 </u>:

1. **[!DNL Inventory module]** を使用した **[!DNL Adobe Commerce]** のインストール
1. **[!UICONTROL Admin]**/**[!UICONTROL Stores]**/**[!UICONTROL Inventory]** に移動し、*2 つのソース* および *2 つの在庫* を作成します。
1. **[!UICONTROL configurable product]** を作成して、**[!UICONTROL default sources]** または **[!UICONTROL newly created sources]** に割り当てます。
1. **[!UICONTROL next button]** をクリックして、製品を *保存* します。
1. 次に、同じ **[!UICONTROL Configurable Product]** を編集し、**[!UICONTROL Configuration tab]** ージ内の **[!UICONTROL Edit Configuration]** をクリックします。
1. `Step 3: Bulk Images,Price and Quantity` に、`price` を変更し、`Quantity` と `Images` をそれぞれ `Skip quantity at this time` と `Skip image uploading at this time` のままにします。
1. 「**[!UICONTROL next button]**」をクリックし、製品を生成します。

<u> 期待される結果 </u>

**[!UICONTROL Configuration tab]** 内のソースごとの数量は空にしないでください。

<u> 実績 </u>

**[!UICONTROL Configuration tab]** 内のソースごとの数量が空です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja>) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja>)」を参照してください。
