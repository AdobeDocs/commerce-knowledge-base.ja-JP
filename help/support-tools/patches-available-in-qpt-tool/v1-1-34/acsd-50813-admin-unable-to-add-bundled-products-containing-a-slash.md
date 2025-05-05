---
title: 「ACSD-50813：管理者が、スラッシュを含むバンドルされた製品を追加できない」
description: ACSD-50813 パッチを適用すると、管理者が、スラッシュ （「/」）を含むバンドル製品を SKU に追加できず、*SKU による製品の追加*機能を管理者の指示に追加できない、Adobe Commerceのパフォーマンスの問題が修正されます。
exl-id: 80dfe877-9dfd-44a9-9bf0-37e929642fc0
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# ACSD-50813：管理者が、スラッシュを含むバンドルされた製品を追加できない

ACSD-50813 パッチにより、管理者が、*[!UICONTROL Add Products by SKU]* 機能を備えた SKU にスラッシュ記号（`/`）を含むバンドル製品を管理注文に追加できない問題が修正されました。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.34 がインストールされている場合に使用できます。 パッチ ID は ACSD-50813 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者は、*[!UICONTROL Add Products by SKU]* 機能を持つ SKU にスラッシュ（`/`）が含まれているバンドル製品を管理注文に追加することはできません。

<u> 再現手順 </u>:

1. **[!UICONTROL Catalog]**/**[!UICONTROL Products]** に移動します。
1. シンプルな製品を作成します。
1. 新しいバンドル製品を作成します。
1. SKU の中央にスラッシュ（`/`）を追加します（例：*Bu/ndle*）。
1. **[!UICONTROL Input Type]** = *[!UICONTROL Dropdown]* のバンドルオプションを追加します。
1. オプションに少なくとも 1 つのシンプルな製品を割り当てます。
1. **[!UICONTROL Sales]**/**[!UICONTROL Orders]** に移動し、新しい注文を作成します。
1. 「**[!UICONTROL Add Products by SKU]**」をクリックします。
1. SKU を入力し、「**[!UICONTROL Add to Order]**」をクリックします。
1. ブラウザーコンソールを開きます。
1. 「**[!UICONTROL Configure]**」をクリックします。

<u> 期待される結果 </u>:

エラーはありません。

<u> 実際の結果 </u>:

コンソールの JS エラー：

*見つからないエラー：構文エラー、認識されない式：div[id=sku_bu/ndle]*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
