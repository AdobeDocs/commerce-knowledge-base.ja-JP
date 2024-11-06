---
title: 「MDVA-40134：共有カタログが有効な場合、GraphQLが関連商品を返さない」
description: MDVA-40134 パッチでは、共有カタログが有効な場合に、GraphQLが関連商品を返さない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.2 がインストールされている場合に利用できます。 パッチ ID は MDVA-40134。 この問題はAdobe Commerce 2.4.3 で修正されました。
exl-id: 7b14355a-1c14-4c80-9426-6c40505d638b
feature: B2B, Catalog Management, GraphQL, Products
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# MDVA-40134：共有カタログが有効な場合、GraphQLが関連商品を返さない

MDVA-40134 パッチでは、共有カタログが有効な場合に、GraphQLが関連商品を返さない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.2 がインストールされている場合に使用できます。 パッチ ID は MDVA-40134。 この問題はAdobe Commerce 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1 - 2.4.2-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

共有カタログが有効になっている場合、GraphQLが関連商品を返さない。

<u> 前提条件 </u>:

B2B モジュールをインストールする必要があります。
インスタンスは、サンプルデータのみでクリーンアップする必要があります。

<u> 再現手順 </u>:

1. **ストア**/**設定**/**一般**/**B2B 機能** に移動し、「**会社および共有カタログ**」を有効にします。
1. **カタログ**/**共有カタログ** に移動し、すべての製品を **一般カタログ** に追加します。
1. サンプルデータを使用して、Jourst Duffle Bag （SKU 24-MB01）を変更します。
1. **関連製品** の下に、2 つのダッフルバッグ（ID 7 と 13）を追加します。
1. **Post** リクエストを送信します。

<pre>{
  製品（フィルター：{sku: {eq: "24-MB01"}}、並べ替え：{name: ASC}） {
    項目 {
      related_products {
        uid
        名前
      }
    }
  }
}</pre>

<u> 期待される結果 </u>:

関連する商品はGraphQLの応答に表示されます。

<u> 実際の結果 </u>:

ユーザーに次のエラーが表示されます。

<pre>Magento\CatalogPermissionsGraphQl\Model\Store\StoreProcessor::getStoreId （）の戻り値は int 型にする必要があり、null は {"exception":"[object] （GraphQL\\Error\\Error （code: 0）:Magento\\CatalogPermissionsGraphQl\\Model\\Store\\StoreProcessor::getStoreId （）の戻り値は int 型にする必要があり、null が返されます </pre>

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
