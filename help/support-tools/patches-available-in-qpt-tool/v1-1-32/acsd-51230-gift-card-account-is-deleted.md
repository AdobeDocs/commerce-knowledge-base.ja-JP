---
title: 「ACSD-51230：ギフトカードアカウントが削除されました」
description: ACSD-51230 パッチを適用すると、簡単な商品の一部の返金が注文から処理されたときにギフトカードのアカウントが削除されるAdobe Commerceの問題を修正できます。
exl-id: 4322a175-3641-468a-8a0f-fcbad90c758f
feature: Customer Service, Gift, Marketing Tools
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# ACSD-51230: ギフト カード アカウントが削除されました

ACSD-51230 パッチは、簡単な商品の一部払い戻しが注文から処理されたときにギフトカードのアカウントが削除される問題を修正します。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.32 がインストールされています。 パッチ ID は ACSD-51230 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

注文から単純商品の一部払い戻しが処理されると、ギフトカード口座は削除されます。

<u>再現手順</u>:

1. での注文の作成 *ギフトカード* および *単純製品* （例： *追加：SKU: GI000XX000XXX、SKU: PC046CP042076*） – （すべての支払いと発送方法が機能します）。
1. 注文を請求します。
1. に移動 **[!UICONTROL Marketing]** > **[!UICONTROL Gift Card accounts]**. ギフトカード用のアカウントが作成されます。
1. 次に進む **[!UICONTROL Order]**&#x200B;を作成し、以下を作成します **[!UICONTROL Credit Memo]**.
1. の数量を変更 *ギフトカード* を 0 に変更して更新します。 これにより、の一部返金が行われます *単純製品*.
1. クリックする **[!UICONTROL Refund]**.
1. 次に、 **[!UICONTROL Marketing]** > **[!UICONTROL Gift Card accounts]**. 新しく作成されたアカウントが削除されます。

<u>期待される結果</u>

ギフトカードに対する払い戻しが作成されなかったため、ギフトカードアカウントを使用できます。

<u>実際の結果</u>

ギフトカードのアカウントは削除され、ギフトカードは払い戻されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
