---
title: 「ACSD-50949：詳細検索の価格フィルターを SKU フィルターと一緒に使用すると、適切な結果が返されません」
description: ACSD-50949 パッチを適用すると、詳細検索で価格フィルターを SKU フィルターと一緒に使用した場合に、適切な結果が返されないAdobe Commerceの問題が修正されます。
feature: Orders, Search
role: Admin
exl-id: 3e1f88dc-07f6-4e10-b4b7-163648076cbc
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 1%

---

# ACSD-50949：詳細検索の価格フィルターを SKU フィルターと共に使用すると、適切な結果が返されない

ACSD-50949 パッチでは、SKU フィルターと一緒に使用した場合に、詳細検索で価格フィルターが適切な結果を返さない問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.33 がインストールされています。 パッチ ID は ACSD-50949 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>). この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 問題

詳細検索の価格フィルターを SKU フィルターと一緒に使用すると、適切な結果が返されません。

<u>再現手順</u>:

1. 複数の製品を作成します。例：

   | SKU | 名前 | 価格 | 数量 |
   |-----|-----------|-------|----------|
   | MJ1 | 製品 1 | $10 | 10 |
   | MJ2 | 製品 2 | $15 | 10 |
   | MJ3 | 製品 3 | $21 | 10 |
   | MJ4 | 製品 4 | $32 | 10 |
   | MJ5 | 製品 5 | $33 | 10 |
   | MJ6 | 製品 6 | $34 | 10 |
   | MJ7 | 製品 7 | $44 | 10 |

1. を開きます **[!UICONTROL Advanced Search]** ストアフロントで、SKU で「MJ」を検索します。
1. 「」をクリックします **[!UICONTROL Modify your search]** リンク。
1. からの条件に価格範囲を追加 *1* 対象： *21*&#x200B;を選択し、 **[!UICONTROL Search]** ボタン。

<u>期待される結果</u>:

定義された範囲内に価格がある製品のみが返されます。

<u>実際の結果</u>:

価格がより高い製品 *$21* が返されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
