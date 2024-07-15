---
title: 「ACSD-55305:[!UICONTROL My Account] で会社のユーザーを編集中にポップアップがフリーズする」
description: ACSD-55305 パッチを適用すると、[!UICONTROL My Account] &gt; [!UICONTROL Company Structure] ページのポップアップ [!UICONTROL Edit Company User] 画面のローダーでフリーズするAdobe Commerceの問題が修正されます。
feature: Companies, B2B
role: Admin, Developer
exl-id: be2bfe08-d05e-485d-84c3-2ff14e1a8654
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# ACSD-55305:[!UICONTROL My Account] で会社のユーザーを編集中にポップアップがフリーズする

ACSD-55305 パッチは、[!UICONTROL My Account]> [!UICONTROL Company Structure] ページのポップアップ [!UICONTROL Edit Company User] 画面のローダーでフリーズする問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.43 がインストールされている場合に使用できます。 パッチ ID は ACSD-55305 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

*[!UICONTROL My Account]*/*[!UICONTROL Company Structure]* ページで *[!UICONTROL Edit Company User]* ポップアップを使用しようとすると、画面にローダーが表示されてフリーズするので、エラーが発生します。

<u> 再現手順 </u>:

1. B2B 会社を作成します。
1. 顧客用に複数選択属性を作成します。
1. 会社管理者の新しく作成した属性に値を割り当てます。
1. 会社管理者としてログインします。
1. [!UICONTROL account dashboard] に移動し、**[!UICONTROL Company Structure]** に移動します。
1. ユーザーを選択します。
1. 「**[!UICONTROL Edit Selected]**」をクリックします。

<u> 期待される結果 </u>:

フォームのポップアップが正確に表示され、会社情報を編集するオプションが表示されます。

<u> 実際の結果 </u>:

フォームのポップアップが表示され、編集することはできません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
