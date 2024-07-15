---
title: 「ACSD-49464：アーカイブから戻されない請求書、出荷およびクレジット・メモ」
description: orderId が異なる場合に請求書、出荷およびクレジットメモがアーカイブから戻されないAdobe Commerceの問題を修正するために、ACSD-49464 パッチを適用します。
exl-id: 845f9878-5f7e-4e58-8f8a-b02af17b3f11
feature: Admin Workspace, Invoices, Orders, Returns, Shipping/Delivery
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# ACSD-49464：アーカイブから戻されない請求書、出荷およびクレジット・メモ

orderId が異なる場合に、請求書、出荷、クレジット メモがアーカイブから戻されない問題は、ACSD-49464 パッチによって修正されます。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.29 がインストールされている場合に使用できます。 パッチ ID は ACSD-49464 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

orderId が異なる場合、請求書、出荷およびクレジット・メモはアーカイブから戻されません。

<u> 再現手順 </u>:

1. 受注、請求書、出荷およびクレジット・メモのアーカイブを使用可能にします。
1. 注文を作成して完了します（出荷、請求書、クレジット メモを含む）。
1. 出荷、請求書、およびクレジット メモの ID が注文番号と同じでないことを確認します。
1. アーカイブする順序を移動します。
1. アーカイブしたオーダーを Order Management に復元します。
1. 各 [!UICONTROL Invoice]、[!UICONTROL Shipping]、[!UICONTROL Credit Memo] のグリッド・ページで、請求書、出荷およびクレジット・メモの詳細を確認します。

<u> 期待される結果 </u>:

オーダーがアーカイブ・リストからオーダー管理に移動されると、元の関連レコードがリストアされます。

<u> 実際の結果 </u>:

* すべての ID が異なる場合、出荷、請求書、およびクレジット メモのレコードはありません。
* 注文と関連レコードの ID が同じ場合、レコードが返されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
