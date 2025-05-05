---
title: 「ACSD-51036:REST API の同時呼び出し時の競合状態によって、出荷ステータスが上書きされる」
description: ACSD-51036 パッチを適用すると、同時に REST API が呼び出され、注文された商品テーブルの配送ステータスが上書きされる際に競合状態が発生するAdobe Commerceの問題を修正できます。
exl-id: 12d90de7-fe5c-4fcc-b84a-d420dcd871ca
feature: REST, Orders, Shipping/Delivery
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# ACSD-51036:REST API の同時呼び出し時の競合状態により、順序付き項目テーブルで出荷ステータスが上書きされます

ACSD-51036 パッチでは、REST API の同時呼び出し時の競合状態によって、順序付き項目テーブルの出荷ステータスが上書きされる問題が修正されています。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.31 がインストールされている場合に使用できます。 パッチ ID は ACSD-51036 です。 この問題はAdobe Commerce 2.4.5 で修正されていることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

REST API の同時呼び出し時の競合状態により、順序付き項目テーブルの出荷ステータスが上書きされます。

<u> 再現手順 </u>:

1. 2 つの項目で注文を作成します。
1. 請求書項目 A.
1. REST API を介して品目 A の払い戻しリクエストを同時に送信すると同時に、品目 B の出荷リクエストを送信します。
1. **[!UICONTROL Admin Panel]** の注文に移動します。

<u> 期待される結果 </u>

*[!UICONTROL Items]* の注文テーブルの品目 B に対して、*[!UICONTROL Shipped 1]* のステータスが存在する必要があります。

<u> 実績 </u>

*[!UICONTROL Items]* 注文テーブルの品目 B に *[!UICONTROL Shipped 1]* のステータスがありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
