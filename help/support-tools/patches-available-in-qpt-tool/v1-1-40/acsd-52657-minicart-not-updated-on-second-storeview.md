---
title: 「ACSD-52657：サブドメインを使用する 2 番目のレビューでミニカートが更新されない」
description: ACSD-52657 パッチを適用すると、サブドメインを使用する 2 番目のストレビューでミニカートが更新されないAdobe Commerceの問題が修正されます。
feature: Shopping Cart
role: Admin, Developer
exl-id: d0877a15-800e-4e10-9ace-ebb7f26dbd18
source-git-commit: f12e25ac5dd607cc614dd99c90c5e104b2cee6a8
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# ACSD-52657: サブドメインを使用する 2 番目の storreview でミニカートが更新されません

ACSD-52657 パッチは、サブドメインを使用する 2 番目のストレビューでミニカートが更新されない問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.40 がインストールされています。 パッチ ID は ACSD-52657 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

サブドメインを使用するセカンダリストアでミニカートが更新されません。

<u>再現手順</u>:

1. 2 つ目のストアレビューを作成し、ベース URL のサブドメインを設定します。
1. cookie ドメインを更新して、共通ドメインを使用します。
1. メインストアで、商品を買い物かごに追加します。
1. 2 番目のストア レビューを更新してから、買い物かごページに移動します。

<u>期待される結果</u>:

買い物かごとミニカートがサブドメインで更新されます。

<u>実際の結果</u>:

ミニカートは、セカンダリストアが更新されても更新されません。ただし、買い物かごページには追加された製品が表示されるので、そのセッションで注文することができます（`PHPSESSID` cookie は共有されます）。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
