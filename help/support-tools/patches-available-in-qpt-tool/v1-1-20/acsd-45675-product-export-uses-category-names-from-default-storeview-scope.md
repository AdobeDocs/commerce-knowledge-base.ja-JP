---
title: 「ACSD-45675：製品のエクスポートで、デフォルトのストア表示範囲のカテゴリ名が使用される」
description: ACSD-45675 パッチでは、製品の書き出しにデフォルトのストア表示範囲のカテゴリ名が使用される問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.20 がインストールされている場合に利用できます。 パッチ ID は ACSD-45675 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: 9edd718e-4c0c-44dd-b802-07c9ec7c182a
feature: Categories, Data Import/Export, Products
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# ACSD-45675：製品のエクスポートで、既定のストア表示範囲のカテゴリ名が使用されます

ACSD-45675 パッチでは、製品の書き出しにデフォルトのストア表示範囲のカテゴリ名が使用される問題が修正されています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.20 がインストールされている場合に使用できます。 パッチ ID は ACSD-45675 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品の書き出しでは、デフォルトのストア表示範囲のカテゴリ名が使用されます。

<u> 再現手順 </u>:

1. カスタムストア表示 **[!UICONTROL Thai]** をメインストア内に作成します。
1. **[!UICONTROL Thai]** をメイン web サイトのデフォルトのストア表示にします。
1. **[!UICONTROL Default Category]** の下に、次のカテゴリ構造を作成します。

   *[!UICONTROL Default category/Tea/Black]*

1. カテゴリ **[!UICONTROL Tea]** を選択し、**[!UICONTROL Scope]** を **[!UICONTROL Thai]** に変更します。
1. **[!UICONTROL Category Name]** を **[!UICONTROL ชาดำ]** に設定します。
1. シンプルな製品 **[!UICONTROL SP001]** を作成し、カテゴリ **[!UICONTROL Black]** を割り当てます。
1. cron が実行されていないことを確認します。
1. 製品を書き出します。 SKU でフィルタリングして、「**[!UICONTROL SP001]**」を選択します。
1. 書き出された CSV の「**[!UICONTROL categories]**」列を確認します。

<u> 期待される結果 </u>:

書き出し時にストアが選択されていなかったので、次のようなカテゴリパスが得られます。*[!UICONTROL Default Category/Tea/Black]*

<u> 実際の結果 </u>:

カテゴリ パスには複数の言語が混在しています：*[!UICONTROL Default Category/ชาดำ/Black]*。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tools] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the Quality Patches Tool Guide
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/patches/check-patch-for-magento-issue-with-magento-quality-patches.html) サポートナレッジベースで確認します。

[!DNL QPT] で使用可能なその他のパッチの詳細については、『品質向上パッチツールガイド』の [ で使用可能なパッチ  [!DNL QPT]](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
