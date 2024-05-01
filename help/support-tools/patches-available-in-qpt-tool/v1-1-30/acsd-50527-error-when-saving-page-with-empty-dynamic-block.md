---
title: 「ACSD-50527：空の動的ブロックを含むページを保存中にエラーが発生しました」
description: ACSD-50527 パッチを適用すると、空の動的ブロックを含んだページを保存する際にエラーが発生するAdobe Commerceの問題を修正できます。
exl-id: 419201f4-7721-47ee-9692-127145f85496
feature: Page Content
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# ACSD-50527：空の動的ブロックを含むページを保存中にエラーが発生しました

ACSD-50527 パッチでは、空の動的ブロックを含むページを保存するとエラーが発生する問題を修正しました。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.30 がインストールされています。 パッチ ID は ACSD-50527 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

空の動的ブロックを含むページを保存すると、エラーが発生します。

<u>再現手順</u>:

1. に移動 **[!UICONTROL Admin]** > **[!UICONTROL Content]** > **[!UICONTROL Dynamic Block]** 空のコンテンツを含む新しい動的ブロックを作成します。
1. に移動 **[!UICONTROL Content]** > **[!UICONTROL Page]** > **[!UICONTROL Create or Edit a new page]**.
1. コンテンツに 2 つの行要素を追加します。 次に、上記で作成した新しいダイナミック ブロックを追加します。

<u>期待される結果</u>:

内に空のコンテンツがあるダイナミックブロックにはエラーは表示されません。 [!DNL Page Builder].

<u>実際の結果</u>:

この [!UICONTROL Dynamic Block] プレースホルダーにエラーが表示されます。

>[!ERROR]
>
>不明なエラーが発生しました。 もう一度やり直してください。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
