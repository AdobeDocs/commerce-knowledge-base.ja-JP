---
title: 「ACSD-54376：商品をから削除した際、買い物かごで例外が発生する [!UICONTROL shared catalog]'
description: ACSD-54376 パッチを適用すると、商品がから削除されたときに買い物かごで例外が発生するAdobe Commerceの問題を修正できます [!UICONTROL shared catalog] カートに追加された後。
feature: Shopping Cart, B2B
role: Admin, Developer
exl-id: a1e5c084-532f-49e8-ab87-6674b44218e8
source-git-commit: 1cc565d5888e5a380c04879d9aced2c19e92c2e5
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# ACSD-54376：商品がから削除された場合に、買い物かごで例外が発生する [!UICONTROL shared catalog]

ACSD-54376 パッチは、製品がから削除されたときに買い物かごで例外が発生する問題を修正します。 [!UICONTROL shared catalog] カートに追加された後。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.41 がインストールされています。 パッチ ID は ACSD-54376 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

商品がから削除されると、買い物かごで例外が発生します [!UICONTROL shared catalog] カートに追加された後。

<u>再現手順</u>:

1. B2B とAdobe Commerceをインストールします。
1. Enable （有効） [!UICONTROL shared catalog].
1. 製品を作成してデフォルトに割り当てる [!UICONTROL shared catalog].
1. ストアフロントから買い物かごに製品を追加します。
1. から製品を削除 [!UICONTROL shared catalog].
1. ミニ買い物かごドロップダウンを使用して、チェックアウトページに移動します。

<u>期待される結果</u>:

例外は処理され、表示されません。

<u>実際の結果</u>:

未処理の例外がチェックアウトページに表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
