---
title: 「ACSD-47988：製品のエクスポートで、ページビルダーの製品説明からHTMLタグがトリミングされる」
description: ACSD-47988 パッチを適用して、製品の書き出しがページビルダーの製品説明からHTMLタグをトリミングするAdobe Commerceの問題を修正してください。
exl-id: 96c45ca8-f526-4876-8f2c-39bce07f86eb
feature: Admin Workspace, Data Import/Export, Page Builder, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# ACSD-47988：商品の書き出しが、ページビルダーのHTML説明から商品タグをトリミングする

ACSD-47988 パッチでは、商品の書き出しでページビルダーの商品説明からHTMLタグがトリミングされる問題が修正されています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.26 がインストールされている場合に使用できます。 パッチ ID は ACSD-47988 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

商品の書き出しは、ページビルダーHTML説明から商品タグをトリミングします。

<u> 再現手順 </u>:

1. 説明にHTMLを含めて商品を作成します。 HTMLタグを挿入するには、ページビルダーHTML要素を使用します。
1. Adobe Commerceの読み込み/書き出し機能を使用した商品の書き出し。
1. 書き出された CSV を読み込みます。
1. 商品を開き、説明の下のHTML要素を確認します。

<u> 期待される結果 </u>:

HTMLタグは、同じコンテンツの読み込み後、商品説明に残ります。

<u> 実際の結果 </u>:

HTMLタグは読み込み後に削除されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
