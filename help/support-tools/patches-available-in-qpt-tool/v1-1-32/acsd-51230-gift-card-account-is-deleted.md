---
title: 「ACSD-51230：ギフトカードアカウントが削除されました」
description: ACSD-51230 パッチを適用すると、簡単な商品の一部の返金が注文から処理されたときにギフトカードのアカウントが削除されるAdobe Commerceの問題を修正できます。
exl-id: 4322a175-3641-468a-8a0f-fcbad90c758f
feature: Customer Service, Gift, Marketing Tools
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# ACSD-51230: ギフト カード アカウントが削除されました

ACSD-51230 パッチは、簡単な商品の一部払い戻しが注文から処理されたときにギフトカードのアカウントが削除される問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.32 がインストールされている場合に使用できます。 パッチ ID は ACSD-51230 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

注文から単純商品の一部払い戻しが処理されると、ギフトカード口座は削除されます。

<u> 再現手順 </u>:

1. *ギフトカード* と *シンプル製品* （例：*追加：SKU:GI000XX000XXX、SKU:PC046CP042076*） – （あらゆる支払いと発送方法で機能）を使用して注文を作成します。
1. 注文を請求します。
1. **[!UICONTROL Marketing]**/**[!UICONTROL Gift Card accounts]** に移動します。 ギフトカード用のアカウントが作成されます。
1. 次に **[!UICONTROL Order]** に移動し、**[!UICONTROL Credit Memo]** を作成します。
1. *ギフトカード* の数量を 0 に変更して更新します。 これにより、*シンプルな製品* の部分払い戻しが作成されます。
1. 「**[!UICONTROL Refund]**」をクリックします。
1. **[!UICONTROL Marketing]** / **[!UICONTROL Gift Card accounts]** を更新します。 新しく作成されたアカウントが削除されます。

<u> 期待される結果 </u>

ギフトカードに対する払い戻しが作成されなかったため、ギフトカードアカウントを使用できます。

<u> 実績 </u>

ギフトカードのアカウントは削除され、ギフトカードは払い戻されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
