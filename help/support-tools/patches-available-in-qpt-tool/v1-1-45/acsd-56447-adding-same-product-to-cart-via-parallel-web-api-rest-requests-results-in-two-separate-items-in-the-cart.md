---
title: 「ACSD-56447：並列 web REST API を使用して同じ製品を買い物かごに追加すると、買い物かごに 2 つの異なる項目が表示される」
description: ACSD-56447 パッチを適用すると、Adobe Commerceの問題を修正できます。この問題では、並行する web REST API リクエストを使用して同じ商品を買い物かごに追加すると、買い物かごに 2 つの異なる商品が表示されます。
feature: Shopping Cart, REST
role: Admin, Developer
exl-id: c63874be-a8a6-4143-adaa-ba3e9e107dd4
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---

# ACSD-56447：並列 web REST API を使用して同じ製品を買い物かごに追加すると、買い物かごに 2 つの異なる項目が表示される

ACSD-56447 パッチでは、並行する web REST API リクエストを介して同じ製品を買い物かごに追加すると、買い物かごに 2 つの異なる項目が表示される問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.45 がインストールされています。 パッチ ID は ACSD-56447 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

並行する web REST API リクエストを使用して同じ製品を買い物かごに追加すると、買い物かごに 2 つの異なる項目が表示されます。

<u>再現手順</u>:

1. を使用して、REST API 呼び出しをリクエストするための顧客トークンを生成します。 [!DNL Postman].
1. 顧客の買い物かごを作成します。
1. 上記で生成したトークンを使用して、顧客用の空の買い物かごを作成します。
1. CURL を使用して 2 つを作成 `AddProductsToCart` 並行して実行されるリクエスト。 の指示に従います [注文処理のチュートリアル](https://developer.adobe.com/commerce/webapi/rest/tutorials/orders/) 開発者向けドキュメント

<u>期待される結果</u>:

複数の数量を持つ品目が 1 行に表示されます。

<u>実際の結果</u>:

複数の行項目で同じ SKU が表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
