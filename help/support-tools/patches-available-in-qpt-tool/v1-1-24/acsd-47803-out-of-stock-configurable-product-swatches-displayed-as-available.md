---
title: 「ACSD-47803：在庫切れの設定可能な製品スウォッチが使用可能として表示される」
description: ACSD-47803 パッチを適用して、在庫切れの設定可能な商品スウォッチが使用可能と表示されるAdobe Commerceの問題を修正してください。
exl-id: 28b3f378-a790-4af6-9627-5bd8571523fd
feature: Configuration, Orders, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# ACSD-47803：在庫切れの設定可能な製品スウォッチが使用可能として表示される

ACSD-47803 パッチでは、在庫切れの設定可能な製品スウォッチが使用可能と表示される問題が修正されています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.24 がインストールされている場合に使用できます。 パッチ ID は ACSD-47803 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

在庫切れの設定可能な製品スウォッチが使用可能として表示されます。

<u> 再現手順 </u>:

>[!NOTE]
>
>以下の手順は、サンプルデータを例として参照します。

1. [!UICONTROL Commerce] Admin で、**[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Catalog]**/**[!UICONTROL Inventory]**/**[!UICONTROL Stock Options]** に移動し、**[!UICONTROL Display Out of Stock Products]** を *はい* に設定します。
1. 再び、管理者から **[!UICONTROL Catalog]** / **[!UICONTROL Products]** に移動して、製品編集ページで設定可能な製品を編集します（サンプルデータを使用している場合は「WB04」 SKU など）。
   * 設定バリアントの 1 つに対して、数量を *0* に設定します（例えば、「WB04-M-Purple」の場合）。
1. 次に、ストアフロントで設定可能な製品を開きます。
1. 在庫が 0 の設定可能なバリアント（つまり「M」）の製品サイズを選択します。

<u> 期待される結果 </u>:

在庫切れオプションは無効になり、[!UICONTROL Out of Stock] としてマークされます。

<u> 実際の結果 </u>:

すべてのカラースウォッチが有効になります（[!UICONTROL Out of Stock] のカラースウォッチも含む）。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
