---
title: 「ACSD-45675：製品のエクスポートで、デフォルトのストア表示範囲のカテゴリ名が使用される」
description: ACSD-45675 パッチでは、製品の書き出しにデフォルトのストア表示範囲のカテゴリ名が使用される問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.20 がインストールされている場合に利用できます。 パッチ ID は ACSD-45675 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: 9edd718e-4c0c-44dd-b802-07c9ec7c182a
feature: Categories, Data Import/Export, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# ACSD-45675：製品のエクスポートで、既定のストア表示範囲のカテゴリ名が使用されます

ACSD-45675 パッチでは、製品の書き出しにデフォルトのストア表示範囲のカテゴリ名が使用される問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.20 がインストールされています。 パッチ ID は ACSD-45675 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品の書き出しでは、デフォルトのストア表示範囲のカテゴリ名が使用されます。

<u>再現手順</u>:

1. カスタムストア表示の作成 **[!UICONTROL Thai]** 本店の中。
1. 作成 **[!UICONTROL Thai]** メイン web サイトのデフォルトのストア表示。
1. 次のカテゴリ構造をの下に作成します。 **[!UICONTROL Default Category]**:

   *[!UICONTROL Default category/Tea/Black]*

1. カテゴリの選択 **[!UICONTROL Tea]** を変更できます **[!UICONTROL Scope]** 対象： **[!UICONTROL Thai]**.
1. を **[!UICONTROL Category Name]** as **[!UICONTROL ชาดำ]**.
1. シンプルな製品の作成 **[!UICONTROL SP001]** カテゴリを割り当てます **[!UICONTROL Black]**.
1. cron が実行されていないことを確認します。
1. 製品を書き出します。 SKU でフィルタリングして選択 **[!UICONTROL SP001]**.
1. を確認します **[!UICONTROL categories]** 書き出された CSV の列。

<u>期待される結果</u>:

書き出し時にストアが選択されていなかったので、次のようなカテゴリパスが得られます。 *[!UICONTROL Default Category/Tea/Black]*.

<u>実際の結果</u>:

カテゴリパスには混合言語があります： *[!UICONTROL Default Category/ชาดำ/Black]*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tools] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) 『品質向上パッチツール』マニュアルの「」を参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/patches/check-patch-for-magento-issue-with-magento-quality-patches.html) サポートナレッジベースで。

で利用可能なその他のパッチについて [!DNL QPT]を参照してください。 [で使用可能なパッチ [!DNL QPT]](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) 『品質向上パッチツール』マニュアルの「」を参照してください。
