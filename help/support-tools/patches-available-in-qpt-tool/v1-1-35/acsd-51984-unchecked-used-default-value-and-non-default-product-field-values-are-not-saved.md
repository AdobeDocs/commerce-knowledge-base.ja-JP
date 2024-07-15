---
title: 「ACSD-51984:2 番目の web サイト、ストア、ストア表示で、オフの [!UICONTROL Use Default Value] とデフォルト以外の製品フィールドの値が保存されない」
description: ACSD-51984 パッチを適用すると、Adobe Commerceの問題を修正できます。この問題では、2 番目の web サイト、ストア、ストアの表示に対して、オフの [!UICONTROL Use Default Value] フィールドとデフォルト以外の製品フィールドの値が保存されません。
feature: Products
role: Admin
exl-id: 1f45c700-dd27-4a69-8634-9c0aa131d197
source-git-commit: f42fcacbe3b7174b2a3571afe80f5eedb8e9aa75
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# ACSD-51984：オフの *[!UICONTROL Use Default Value]* とデフォルト以外の製品フィールド値は保存されない

>[!NOTE]
>
>このパッチは古く、1.1.39 QPT リリースで追加された [ACSD-54776](/help/support-tools/patches-available-in-qpt-tool/v1-1-39/acsd-54776-unchecked-used-default-value-and-non-default-product-field-values-are-not-saved.md) パッチに置き換えられました。

ACSD-51984 パッチを使用すると、2 番目の web サイト、ストア、ストアの表示で、オフの **[!UICONTROL Use Default Value]** フィールドとデフォルト以外の製品フィールドの値が保存されない問題を修正できます。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.35 がインストールされている場合に使用できます。 パッチ ID は ACSD-51984 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

オフにした場合 *[!UICONTROL Use Default Value]* デフォルト以外の製品フィールドの値は、2 番目の web サイト、ストア、ストアの表示では保存されません。

<u> 再現手順 </u>:

1. バックエンドに移動し、**[!UICONTROL Stores]**/**[!UICONTROL All Stores]** に移動して、新しい web サイト、ストア、ストア表示を作成します。
1. **[!UICONTROL Catalog]**/**[!UICONTROL Products]** に移動してシンプルな製品を作成して保存し、**[!UICONTROL Product in Websites]** から両方の web サイトに製品を割り当てます。
1. 手順 2 で新しく作成したストア表示に範囲を変更します。
1. **[!UICONTROL Search Engine Optimization]** に移動し、[!UICONTROL Meta Title]、[!UICONTROL Meta Keywords]、[!UICONTROL Meta Description] の **[!UICONTROL Use Default Value]** のチェックボックスをオフにします。
1. フィールド（*[!UICONTROL Meta Title]*、*[!UICONTROL Meta Keywords]*、*[!UICONTROL Meta Description]*）からテキストを消去し、「**[!UICONTROL Save]**」をクリックします。
1. もう一度 **[!UICONTROL Search Engine Optimization]** に移動します。

<u> 期待される結果 </u>

フィールドの値とチェックボックスの値が保存されます。

<u> 実績 </u>

フィールドとチェックボックスの値は保存されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html>) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>)」を参照してください。