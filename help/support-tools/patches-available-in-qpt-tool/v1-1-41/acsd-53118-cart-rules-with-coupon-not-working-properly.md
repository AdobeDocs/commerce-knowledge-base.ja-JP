---
title: 「ACSD-53118：クーポンのある買い物かごルールが正しく機能しない」
description: ACSD-53118 パッチを適用すると、カート内の商品に空の一致属性がある場合に、クーポンコードを使用してカートの価格ルールが適用されるAdobe Commerceの問題を修正できます。
feature: Shopping Cart, Price Rules
role: Admin, Developer
exl-id: a660ddb3-03fc-4460-b2a8-8e851f57e7a9
source-git-commit: 35cd21581ee34a6213be42a79e159439b8856fb6
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# ACSD-53118：クーポンのある買い物かごルールが正しく機能しない

ACSD-53118 パッチは、カート内の製品に空の一致属性がある場合に、クーポンコードを使用してカートの価格ルールが適用される問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.41 がインストールされています。 パッチ ID は ACSD-53118 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

買い物かごの商品に空の一致する属性がある場合、買い物かごの価格ルールはクーポンコードを使用して適用されます。

<u>再現手順</u>:

1. 価格属性を作成し、属性セットに追加します。 プロモルール条件で属性を使用できるようにします。
1. 製品を作成し、新しい属性は空のままにします。
1. 特定のクーポンと次の条件を持つ買い物かご価格ルールを作成します。

   * 買い物かごで項目が見つかり、そのすべての条件が true の場合、属性 1 は 0 です。

1. 手順 2 で作成した商品を買い物かごに追加します。
1. 手順 3 で作成した買い物かごルールにクーポンコードを使用します。

<u>期待される結果</u>:

割引は買い物かごには適用されません。

<u>実際の結果</u>:

買い物かごには割引が適用されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
