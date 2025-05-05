---
title: 「ACSD-54989:[!UICONTROL Enable Purchase Orders] が「はい」に設定され、[!UICONTROL Purchase Order] が「いいえ」に設定されている場合、会社管理者が注文できない」
description: ACSD-54989 パッチを適用すると、[!UICONTROL Enable Purchase Orders] が Yes に、[!UICONTROL Purchase Order] が No に設定されている場合に、会社管理者が注文できないAdobe Commerceの問題を修正できます。
feature: Orders, Companies, Purchase Orders
role: Admin, Developer
exl-id: c2850409-d310-4681-80ec-af8ba347854c
source-git-commit: 35cd21581ee34a6213be42a79e159439b8856fb6
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# ACSD-54989：会社管理者は、*[!UICONTROL Enable Purchase Orders]* ーザーが *はい*、*[!UICONTROL Purchase Order]* が *いいえ* に設定されている場合、注文できません

ACSD-54989 パッチは、**[!UICONTROL Enable Purchase Orders]** が *Yes* に設定され、**[!UICONTROL Purchase Order]** が *No* に設定されている場合に注文できない問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.40 がインストールされている場合に使用できます。 パッチ ID は ACSD-54989 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p5 - 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

会社管理者は、**[!UICONTROL Enable Purchase Orders]** が *はい* および **発注書** が *いいえ* に設定されている場合、注文を行うことはできません。

<u> 前提条件 </u>:

[!DNL B2B] モジュールをインストールします。

<u> 再現手順 </u>:

1. 会社を有効にし、[!UICONTROL **Order Approval Configuration]** > **[!UICONTROL Purchase Order**] = *いいえ* のままにします。
1. 100 の価格で簡単な製品を作成してください。
1. 管理者を通じて会社を新規作成します。
1. [!UICONTROL **発注の有効化**] を *Yes* に設定します。
1. ストアフロントで会社管理者としてログインします。
1. 作成したシンプルな製品を買い物かごに追加します。
1. チェックアウトページに進み、「**[!UICONTROL Place Order]**」をクリックして購入を完了します。

<u> 期待される結果 </u>:

注文は正常に行えます。

<u> 実際の結果 </u>:

**[!UICONTROL My Account]** ページが開き、注文は行われません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
