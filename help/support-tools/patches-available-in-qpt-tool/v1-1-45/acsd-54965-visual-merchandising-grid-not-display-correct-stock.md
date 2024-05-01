---
title: 'ACSD-54965: [!UICONTROL Visual Merchandising] グリッドに正しい素材が表示されません'
description: Adobe Commerce ACSD-54965 パッチを適用して、 [!UICONTROL Visual Merchandising] 製品がカスタム在庫に割り当てられているときに、グリッドに正しい在庫が表示されない。
feature: Merchandising, Categories
role: Admin, Developer
exl-id: 13d98f55-ca2c-4064-b66f-ab2cdeb37382
source-git-commit: 4f05117aa42dec1f56e4986ffd22d1a68bf5cea2
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# ACSD-54965: [!UICONTROL Visual Merchandising] グリッドに正しい素材が表示されない

ACSD-54965 パッチは、 [!UICONTROL Visual Merchandising] 製品がカスタム在庫に割り当てられているときに、グリッドに正しい在庫が表示されない。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.45 がインストールされています。 パッチ ID は ACSD-54965 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.5-p5

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

この [!UICONTROL Visual Merchandising] 製品がカスタム在庫に割り当てられているときに、グリッドに正しい在庫が表示されない。

<u>再現手順</u>:

1. 新規ソースを作成します。
1. 新しい在庫を作成します。
1. 2 つの製品を作成します。
   * カスタム在庫のみを持つ 1 つの製品。
   * デフォルトの在庫のみを持つ製品。
1. これらの製品をカテゴリに追加します。
1. に移動します [!UICONTROL visual Merchandising] グリッド （*[!UICONTROL Products in Category]*）に設定します。

<u>実際の結果</u>:

が含まれる *[!UICONTROL All Store Views]* 範囲、カスタム在庫のある製品には数量は表示されません。 次の場合のみ *[!UICONTROL Default Store View]* 範囲の選択カスタム在庫は製品の数量を表示します。

<u>期待される結果</u>:

グリッドは、範囲がの場合、すべての在庫情報を表示します。 *[!UICONTROL All Store Views]*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
