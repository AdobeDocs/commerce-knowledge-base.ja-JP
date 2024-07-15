---
title: 「ACSD-50345：チェックアウト中の reCAPTCHA の問題」
description: ACSD-50345 パッチを適用すると、注文処理中およびチェックアウト中に reCAPTCHA v2 と v3 の検証が失敗するAdobe Commerceの問題を修正できます。
exl-id: ac8c8130-0e4d-4610-9a55-afa779cce7a0
feature: Checkout, Orders
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# ACSD-50345：チェックアウト中の reCAPTCHA の問題

ACSD-50345 パッチは、注文処理中およびチェックアウト中に reCAPTCHA v2 と v3 の検証が失敗する問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.31 がインストールされている場合に使用できます。 パッチ ID は ACSD-50345 です。 この問題はAdobe Commerce 2.4.6 で部分的に修正され、Adobe Commerce 2.4.7 で完全に修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.5-p2

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

**事例#1**

Google reCAPTCHA v2 が、支払いに失敗した後、リロードされない。

<u> 再現手順 </u>

1. **[!UICONTROL Google reCAPTCHA v2]** を設定します *私はロボットではありません*）。
1. チェックアウトの **[!UICONTROL reCAPTCHA]** を有効にします。
1. **[!UICONTROL reCAPTCHA]** をクリックせずに注文してみてください。
1. ユーザーが欠落している reCAPTCHA に関するエラーメッセージを受け取ったら（*reCAPTCHA 検証に失敗しました。もう一度試してください*）、**[!UICONTROL reCAPTCHA]** をクリックして注文を試します。

<u> 期待される結果 </u>

間違った reCAPTCHA で注文されることはありません。

<u> 実績 </u>

エラーがスローされました – *reCAPTCHA 検証に失敗しました。もう一度試してください* と *ID = 4 のそのような買い物かごはありません*

**事例#2**

Google reCAPTCHA v3 Invisible がチェックアウト時に機能せず、注文できません。 `PlaceOrder` イベントはトリガーされません。

<u> 再現手順 </u>

1. **[!UICONTROL Store]**/**[!UICONTROL Configuration]**/**[!UICONTROL Security]** から **[!UICONTROL reCAPTCHA v3 Invisible]** を設定します。
1. 「**[!UICONTROL Storefront]**」タブで、注文のチェックアウト/発注の **[!UICONTROL reCAPTCHA v3 Invisible]** を有効にします。
1. [!UICONTROL Check/Money order] の支払い方法で注文してみてください。

<u> 期待される結果 </u>

**[!UICONTROL reCAPTCHA]** をオンにして注文する必要があります。

<u> 実績 </u>

**[!UICONTROL Place Order]** ボタンをクリックすると、無効になり、それ以上何も起こりません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
