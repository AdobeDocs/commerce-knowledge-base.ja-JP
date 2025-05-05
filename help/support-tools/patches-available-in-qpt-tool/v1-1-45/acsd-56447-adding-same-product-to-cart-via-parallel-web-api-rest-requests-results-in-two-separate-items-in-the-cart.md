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

ACSD-56447 パッチでは、並行する web REST API リクエストを介して同じ製品を買い物かごに追加すると、買い物かごに 2 つの異なる項目が表示される問題が修正されています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.45 がインストールされている場合に使用できます。 パッチ ID は ACSD-56447 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

並行する web REST API リクエストを使用して同じ製品を買い物かごに追加すると、買い物かごに 2 つの異なる項目が表示されます。

<u> 再現手順 </u>:

1. [!DNL Postman] を使用して REST API 呼び出しリクエストを行うための顧客トークンを生成します。
1. 顧客の買い物かごを作成します。
1. 上記で生成したトークンを使用して、顧客用の空の買い物かごを作成します。
1. CURL を使用すると、並行して実行される 2 つの `AddProductsToCart` リクエストを作成できます。 開発者向けドキュメントの [ 注文処理のチュートリアル ](https://developer.adobe.com/commerce/webapi/rest/tutorials/orders/) の手順に従います。

<u> 期待される結果 </u>:

複数の数量を持つ品目が 1 行に表示されます。

<u> 実際の結果 </u>:

複数の行項目で同じ SKU が表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
