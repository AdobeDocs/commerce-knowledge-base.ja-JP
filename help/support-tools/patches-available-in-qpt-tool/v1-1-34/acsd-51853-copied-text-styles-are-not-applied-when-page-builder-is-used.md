---
title: 「ACSD-51853：コピーしたテキストスタイルがページビルダーを使用して適用されない」
description: ACSD-51853 パッチを適用すると、ページビルダーを使用したときにコピーしたテキストスタイルが適用されないAdobe Commerceの問題が修正されます。
feature: Page Builder
role: Admin
exl-id: 1efd3147-1ae0-468b-af04-1632fbaaefda
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# ACSD-51853：コピーしたテキストスタイルは、ページビルダーを使用して適用されない

ACSD-51853 パッチでは、ページビルダーを使用したときに、コピーしたテキストスタイルが適用されない問題を修正しています。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.34 がインストールされています。 パッチ ID は ACSD-51853 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1 ～ 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

コピーしたテキストスタイルは、ページビルダーが使用されている場合は適用されません

<u>再現手順</u>:

1. 管理者にログインします。
1. /に移動します。 **コンテンツ** > **ページ** > **ページを開く** > **ページビルダーで編集**.
1. 行をドラッグ *テキスト* から **[!UICONTROL Elements]**.
1. コピー **エンリッチドコンテンツ**&#x200B;そのテキストをに貼り付けます **[!UICONTROL Page Builder]**.

<u>期待される結果</u>

コピーしたテキストは、すべてのスタイルと共に貼り付けられます。

<u>実際の結果</u>

コピーされたテキストはプレーンテキストとして貼り付けられ、すべてのスタイルが失われます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
