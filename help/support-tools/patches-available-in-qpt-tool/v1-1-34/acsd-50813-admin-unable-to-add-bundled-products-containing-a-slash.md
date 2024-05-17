---
title: 「ACSD-50813：管理者が、スラッシュを含むバンドルされた製品を追加できない」
description: ACSD-50813 パッチを適用すると、管理者が、スラッシュ （「/」）を含むバンドル製品を SKU に追加できず、*SKU による製品の追加*機能を管理者の指示に追加できない、Adobe Commerceのパフォーマンスの問題が修正されます。
exl-id: 80dfe877-9dfd-44a9-9bf0-37e929642fc0
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# ACSD-50813：管理者が、スラッシュを含むバンドルされた製品を追加できない

ACSD-50813 パッチにより、管理者がスラッシュ記号（`/`）が表示されます。 *[!UICONTROL Add Products by SKU]* 管理注文に対する機能。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.34 がインストールされています。 パッチ ID は ACSD-50813 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者が、スラッシュ（`/`）が表示されます。 *[!UICONTROL Add Products by SKU]* 管理注文に対する機能。

<u>再現手順</u>:

1. に移動 **[!UICONTROL Catalog]** > **[!UICONTROL Products]**.
1. シンプルな製品を作成します。
1. 新しいバンドル製品を作成します。
1. スラッシュ（`/`）が SKU の途中にあります（例： *バンドル/バンドル*）に設定します。
1. にバンドルされたオプションを追加する **[!UICONTROL Input Type]** = *[!UICONTROL Dropdown]*.
1. オプションに少なくとも 1 つのシンプルな製品を割り当てます。
1. に移動 **[!UICONTROL Sales]** > **[!UICONTROL Orders]**&#x200B;をクリックし、新しい注文を作成します。
1. クリックする **[!UICONTROL Add Products by SKU]**.
1. SKU を入力し、 **[!UICONTROL Add to Order]**.
1. ブラウザーコンソールを開きます。
1. クリックする **[!UICONTROL Configure]**.

<u>期待される結果</u>:

エラーはありません。

<u>実際の結果</u>:

コンソールの JS エラー：

*不明なエラー：構文エラー、認識されない式：div[id=sku_bu/ndle]*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
