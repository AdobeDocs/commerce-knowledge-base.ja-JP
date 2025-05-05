---
title: 「ACSD-53636：通常の価格がページに表示さ [!UICONTROL Product Listing] ない」
description: 特別価格の子商品を持つ設定可能な商品の*[!UICONTROL Product Listing]* ページに通常価格が表示されないAdobe Commerceの問題を修正するために、ACSD-53636 パッチを適用してください。
feature: Catalog Management, Products
role: Admin, Developer
exl-id: 97b4eb64-92d1-4db1-8e5b-915b16115663
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# ACSD-53636：通常の価格がページに表示さ *[!UICONTROL Product Listing]* ない

ACSD-53636 パッチは、特別価格の子製品を持つ設定可能な製品の *[!UICONTROL Product Listing]* ページに通常価格が表示されない問題を修正しました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.43 がインストールされている場合に使用できます。 パッチ ID は ACSD-53636 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.4-p6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

特別価格を持つ子製品を持つ設定可能な製品の *[!UICONTROL Product Listing]* ページには、通常価格は表示されません。

<u> 再現手順 </u>:

1. 管理者にログインして **[!UICONTROL Admin]**/**[!UICONTROL Catalog]** に移動し、設定可能な製品を作成するか開きます。
2. 子製品を開き、すべてまたは 1 つの子製品に特別価格を追加して、製品を保存します。
3. フロントエンドに移動し、設定可能な製品の **[!UICONTROL Product Detail]** ページを開きます。特別価格の子製品のスウォッチには、（期待される） *[!UICONTROL Regular price]* が取り除かれています。
4. フロントエンドに移動し、特別価格の設定可能な製品の **[!UICONTROL Product Listing]** ページを開きます。*[!UICONTROL Product Detail Page]* やその他のシンプルな製品とは異なり、設定可能な製品スウォッチの変更に通常の価格が表示されないことを確認してください。

<u> 期待される結果 </u>:

*[!UICONTROL Product Listing]* ページでは、設定可能な製品には、子製品の通常の価格が表示されます。

<u> 実際の結果 </u>:

*[!UICONTROL Product Listing]* ページで、設定可能な製品には、子製品の通常の価格は表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
