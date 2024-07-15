---
title: 「ACSD-57854:*GraphQL*応答に、カテゴリ集計にリストされるべきでない無効なカテゴリが含まれています」
description: ACSD-57854 パッチを適用して、*GraphQL*応答に、カテゴリ集計にリストされるべきでない無効なカテゴリが含まれているAdobe Commerceの問題を修正してください。
feature: GraphQL
role: Admin, Developer
exl-id: b6130a0f-57bc-4719-99f2-beb630c463c7
source-git-commit: ea6f23a7ce599e24c6b683f82cf08b72b2506020
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# ACSD-57854: *GraphQL* 応答に、カテゴリ集計に表示されるべきではない、無効なカテゴリが含まれています

ACSD-57854 パッチは、*GraphQL* レスポンスに、カテゴリ集計にリストされるべきではない無効なカテゴリが含まれている問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.48 がインストールされている場合に使用できます。 パッチ ID は ACSD-57854 です。 この問題はAdobe Commerce 2.5.0 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p4

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

*GraphQL* の応答に、カテゴリ集計にリストすべきでない、無効なカテゴリが含まれています。

<u> 再現手順 </u>:

1. 2 つのカテゴリを作成します。
1. 商品（テストAdobe商品）を作成して、商品を両方のカテゴリに割り当てます。
1. 作成されたカテゴリの 1 つを無効にします。
1. 商品 *GraphQL* を使用して商品を検索します。
1. *GraphQL* レスポンスの商品カテゴリのリストを確認します。

<u> 期待される結果 </u>:

無効になっているカテゴリは、*GraphQL* 応答に含まれていません。

<u> 実際の結果 </u>:

無効なカテゴリはカテゴリ集計 *GraphQL* 応答に一覧表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
