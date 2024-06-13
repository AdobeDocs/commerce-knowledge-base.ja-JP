---
title: 「ACSD-56546：設定可能な製品とバンドル製品が、ストアフロントに在庫切れとして表示される」
description: Adobe Commerce ACSD-56546 パッチを適用すると、設定可能な製品とバンドル製品がストアフロントで*[!UICONTROL Display Out of Stock Products]*設定オプションが無効になっています。
feature: Storefront, Products
role: Admin, Developer
exl-id: 488e2c69-442f-45e1-aa8f-71d9c0a93950
source-git-commit: 031d5cad6727bac61c88f21fa7c84e0d2a6df331
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# ACSD-56546：設定可能な製品およびバンドル製品が、ストアフロントに在庫切れとして表示される

ACSD-56546 パッチでは、設定可能な製品とバンドル製品がストアフロントに在庫切れとして表示される問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.48 がインストールされています。 パッチ ID は ACSD-56546 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

設定可能な製品とバンドル製品は、次の場合にストアフロントに在庫切れとして表示されます *[!UICONTROL Display Out of Stock Products]* オプションは無効です。

<u>再現手順</u>:

1. を **[!UICONTROL Display Out of Stock Products]** 対するオプション *不可*.
1. Web サイト、ストア、ストアレビューを作成します。
1. ソースと在庫を作成して、2 番目の web サイトに割り当てます。
1. を作成 *設定可能な製品* 2 つの子製品を持つ。 子製品を両方のソースと両方の web サイトに割り当てます。
1. 最初の子製品を更新してを持たせる *数量=0* 両方のソース。
1. 2 つ目の子製品を更新し、2 つ目の web サイトで無効にします。
1. 完全な再インデックスを実行します。
1. 2 番目の web サイトで、設定可能な製品を含むカテゴリを確認します。

<u>期待される結果</u>:

在庫切れの設定可能な製品は、ストアフロントには表示されません。

<u>実際の結果</u>:

在庫切れの設定可能な製品は、 *[!UICONTROL Display Out of Stock Products]* オプションは無効です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
