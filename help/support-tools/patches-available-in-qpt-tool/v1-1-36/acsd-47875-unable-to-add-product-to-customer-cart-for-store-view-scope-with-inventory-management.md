---
title: 「ACSD-47875：在庫管理を使用した店舗表示範囲の買い物かごに製品を追加できない」
description: ACSD-47875 パッチを適用すると、在庫管理の特定のストア表示範囲で、管理者から商品を買い物かごに追加できないAdobe Commerceの問題を修正できます。
feature: Inventory, Shopping Cart, Products
role: Admin, Developer
exl-id: fa5ecd65-704f-49bd-b3cc-3d60ff7e1dce
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# ACSD-47875：在庫管理を使用したストア表示範囲の買い物かごに製品を追加できない

ACSD-47875 パッチを使用すると、在庫管理の特定のストア表示範囲に対して管理者から製品を顧客の買い物かごに追加できない問題を修正できます。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.36 がインストールされています。 パッチ ID は ACSD-47875 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者ユーザーが、を使用して顧客の買い物かごに製品を追加できない **[!UICONTROL Manage Shopping Cart]** msi がインストールされた特定のストア表示範囲の管理機能。

<u>前提条件</u>:

[!DNL Adobe Commerce Inventory Management (MSI)] モジュールがインストールされ、有効になっています。

<u>再現手順</u>:

1. Web サイト、ストア、ストアビューを作成します。
1. 以外の追加のソースを作成 *デフォルト*.
1. 新しい在庫を作成し、新しい web サイトと新しいソースに割り当てます。
1. 新しい web サイトの新しい顧客を作成します。
1. 新しい web サイトにのみ製品を割り当て、デフォルトの web サイトから割り当てを解除します。

   * 新しいソースを割り当てて数量を設定 *0 より上* 新しいソース用およびの場合 *0* をデフォルトソースとして使用します。

1. に移動します **[!UICONTROL Customer Edit]** 管理画面の「」ページ。 クリック **[!UICONTROL Manage Shopping Cart]**.
1. ストア表示の範囲を新しいストア表示に変更します。
1. に移動します **[!UICONTROL Products]** 「」セクションをクリックして、製品を検索します。
1. 製品を選択し、 **[!UICONTROL Add selections to my cart]**.

<u>期待される結果</u>:

商品が買い物かごに追加されます。

<u>実際の結果</u>:

* 次のエラーが発生します。 *追加しようとしている製品は利用できません。*
* 商品は買い物かごに追加されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
