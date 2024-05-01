---
title: '''ACSD-46767: [!UICONTROL Category] 「在庫数が変更されると、ページキャッシュが無効になる」'
description: Adobe Commerce ACSD-46767 パッチを適用して、 [!UICONTROL Category] 商品がまだ在庫にある場合でも、在庫数が変更されると、ページキャッシュは無効になります。
feature: Cache, Products, Inventory
role: Admin, Developer
exl-id: 39811c03-8518-4975-a128-31537b4706c0
source-git-commit: b7e2ff7cd259963adb9a113eb8e94acdaa45ba1e
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---

# ACSD-46767: [!UICONTROL Category] 在庫数が変更されると、ページキャッシュが無効になります

ACSD-46767 パッチは、 [!UICONTROL Category] 商品がまだ在庫にある場合でも、在庫数が変更されると、ページキャッシュは無効になります。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.46 がインストールされています。 パッチ ID は ACSD-46767 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.5-p5

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

[!UICONTROL Category] 在庫数が変更されると、ページキャッシュは無効になります。

<u>再現手順</u>:

1. いくつかの製品を作成して、同じカテゴリに追加します。
1. を開きます *[!UICONTROL Category]* ストアフロントの「」ページに移動して、ページがキャッシュされるようにします。
1. カテゴリの製品のいずれかを使用して注文します *（製品数量は変更されますが、製品はまだ在庫があります）*.
1. を開きます [!UICONTROL Category] もう一度ストアフロントのページ。

<u>実際の結果</u>:

キャッシュからページが読み込まれない。 再生成されます。

<u>期待される結果</u>:

ページがキャッシュから読み込まれます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
