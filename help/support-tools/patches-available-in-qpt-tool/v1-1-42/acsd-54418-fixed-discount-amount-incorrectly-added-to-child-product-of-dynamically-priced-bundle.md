---
title: 「ACSD-54418：動的に価格設定されたバンドルの子製品に誤って追加された固定割引額」
description: ACSD-54418 パッチを適用すると、動的に価格が設定されるバンドルの各子製品に固定割引額が誤って適用されるAdobe Commerceの問題を修正できます。
feature: Shopping Cart
role: Admin, Developer
exl-id: f9a00a4b-0a57-4a61-8b7c-6385e0751991
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# ACSD-54418：動的に価格設定されたバンドルの子製品に、誤って追加された固定割引額。

ACSD-54418 パッチでは、動的に価格設定されたバンドルの各子製品に固定割引額が誤って適用される問題が修正されています。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.42 がインストールされています。 パッチ ID は ACSD-54418 です。 この問題はAdobe Commerce 2.4.7 で修正されていることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

固定割引額が、動的に価格設定されたバンドルの各子製品に誤って適用されます。

<u>再現手順</u>:

1. を作成 **[!UICONTROL bundle product]** 動的な価格設定と *2* バンドルオプション。
1. を作成 **[!UICONTROL cart price rule]** バンドルされた製品にのみ適用される特定のクーポンコードを使用 **[!UICONTROL SKU]** およびは固定割引です。
1. バンドルされた製品を買い物かごに追加します。
1. を適用 **[!UICONTROL coupon code]**.
1. 買い物かごに適用される割引を確認します。

<u>期待される結果</u>:

割引は、バンドルされた製品全体に 1 回だけ適用されます。

<u>実際の結果</u>:

割引は、各バンドル子製品に適用されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
