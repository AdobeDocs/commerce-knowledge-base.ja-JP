---
title: 「ACSD-52095:CSV の書き出し中に、在庫値の管理が間違っています」
description: CSV の書き出し中に商品の在庫管理方法で値が間違っていたAdobe Commerceの問題を修正するために、ACSD-52095 パッチを適用してください。
feature: Inventory, Products
role: Admin, Developer
exl-id: 9e599931-e9b1-4216-b78d-3993d9c3132d
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# ACSD-52095:CSV の書き出し中に [!UICONTROL Manage Stock] の値が間違っている

ACSD-52095 パッチは、CSV の書き出し中に製品 `manage_stock` の値が間違っていた問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.35 がインストールされている場合に使用できます。 パッチ ID は ACSD-52095 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.5-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品の書き出し後、CSV ファイルで `manage_stock` の値が正しく 0 に設定されません。

<u> 再現手順 </u>:

1. **[!UICONTROL Admin]**/**[!UICONTROL Store]**/**[!UICONTROL Configuration]**/**[!UICONTROL Catalog]**/**[!UICONTROL Inventory]**/**[!UICONTROL Product Stock Options]** に移動し、**[!UICONTROL Manage Stock]** = *[!UICONTROL No]* を設定します。
1. 新しい製品を作成して保存します。
1. **[!UICONTROL System]**/**[!UICONTROL Export]** に移動します。
1. *[!UICONTROL Entity Type]* = *[!UICONTROL Products]* を選択し、製品を書き出します。
1. 生成された CSV ファイル（`manage_stock` = 0、`use_config_manage_stock` = 1）を確認します。
1. もう一度 **[!UICONTROL Admin]**/**[!UICONTROL Store]**/**[!UICONTROL Configuration]**/**[!UICONTROL Catalog]**/**[!UICONTROL Inventory]**/**[!UICONTROL Product Stock Options]** に移動し、**[!UICONTROL Manage Stock]** = *[!UICONTROL Yes]* を設定します。
1. **システム**/**エクスポート** に移動します。
*[!UICONTROL Entity Type]* = *[!UICONTROL Products and export the products]* を選択します。
1. 生成された CSV ファイル（`manage_stock` = 0、`use_config_manage_stock` = 1）を確認します。
1. 管理者で製品を開き、**[!UICONTROL Advanced Inventory]** に移動して **[!UICONTROL Manage Stock]** の値を確認します。

<u> 期待される結果 </u>

製品に対して有効な場合、**[!UICONTROL Manage Stock]** の値は *1* です。

<u> 実績 </u>

製品に対して有効な場合、**[!UICONTROL Manage Stock]** の値は *0* になります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html>) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>)」を参照してください。
