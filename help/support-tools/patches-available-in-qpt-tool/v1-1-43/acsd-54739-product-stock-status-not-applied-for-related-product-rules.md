---
title: 'ACSD-54739: *[!UICONTROL Product Stock]* ステータスが*[!UICONTROL Related Product Rules]*に適用されていません'
description: ACSD-54739 パッチを適用して、*[!UICONTROL Product Stock]* ステータスが*[!UICONTROL Related Product Rules]*に適用されないAdobe Commerceの問題を修正してください。
feature: Products
role: Admin, Developer
exl-id: 7bc106b1-2c97-46a1-8bb6-71b99511e480
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# ACSD-54739:*[!UICONTROL Product stock]* ステータスが *[!UICONTROL Related Product Rules]* に適用されない

ACSD-54739 パッチは、*[!UICONTROL Product stock]* ステータスが *[!UICONTROL Related Product Rules]* に適用されない問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.43 がインストールされている場合に使用できます。 パッチ ID は ACSD-54739 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.5-p5

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

*[!UICONTROL Product stock]* ステータスが *[!UICONTROL Related Product Rules]* に適用されていません。

<u> 再現手順 </u>:

1. **[!UICONTROL Display Out of Stock Products]** 設定を *はい* に設定します。
1. **[!UICONTROL Admin]**/**[!UICONTROL Stores]**/**[!UICONTROL Attributes]**/**[!UICONTROL Product]**/**[!UICONTROL Search quantity attribute]** に移動し、プロモーションルールの条件に *はい* を設定します。
1. 関連製品ルールを作成します。 **[!UICONTROL Product rule information]**/**[!UICONTROL Products to match]**/属性数量を含む条件を追加に移動します（在庫切れ/在庫切れを選択）。
1. フロントエンドの製品を確認します。

<u> 期待される結果 </u>:

在庫品/在庫切れの商品は、*[!UICONTROL Related Product Rules]* で一致します。

<u> 実際の結果 </u>:

在庫/在庫切れの商品が *[!UICONTROL Related Product Rules]* に一致しません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
