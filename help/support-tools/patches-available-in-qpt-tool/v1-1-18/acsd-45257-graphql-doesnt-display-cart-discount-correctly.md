---
title: 「ACSD-45257:GraphQLで買い物かごの割引が正しく表示されない」
description: ACSD-45257 パッチを適用すると、GraphQLに買い物かごの割引が正しく表示されない問題が修正されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.18 がインストールされている場合に利用できます。 パッチ ID は ACSD-45257 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: 64576fa3-1160-4fc3-8458-4e622c30af74
feature: GraphQL, Marketing Tools, Orders, Personalization, Shopping Cart
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# ACSD-45257:GraphQLで買い物かごの割引が正しく表示されない

ACSD-45257 パッチを適用すると、GraphQLに買い物かごの割引が正しく表示されない問題が修正されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.18 がインストールされている場合に使用できます。 パッチ ID は ACSD-45257 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.4 - 2.4.3-p3

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

GraphQLに買い物かごの割引が正しく表示されません。

<u> 再現手順 </u>:

1. **管理者**/**マーケティング**/**プロモーション**/**買い物かご価格ルール** に移動します。
1. 新しいルールを追加し、出荷金額に適用します。
1. GraphQLを使用して買い物かごに商品を追加する。
1. GraphQL クエリを使用して買い物かご情報を確認します。

<u> 期待される結果 </u>:

割引合計には、GraphQL応答で配送料に適用される割引が含まれます。

<u> 実際の結果 </u>:

合計割引額は、GraphQLの応答で配送料に適用される割引額を反映していません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
