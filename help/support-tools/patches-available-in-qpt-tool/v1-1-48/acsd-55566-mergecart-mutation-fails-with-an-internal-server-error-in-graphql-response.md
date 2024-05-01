---
title: 'ACSD-55566: [!UICONTROL mergeCart] 内部サーバーエラーでミューテーションが失敗する [!DNL GraphQL] response'
description: ACSD-55566 パッチを適用すると、の内部サーバーエラーで「mergeCart」ミューテーションが失敗するAdobe Commerceの問題を修正できます。 [!DNL GraphQL] 同じバンドル項目を持つソースと宛先の買い物かごを結合する場合の応答。
feature: GraphQL, Shopping Cart
role: Admin, Developer
exl-id: 84a9b861-351e-4fcc-bb91-3e31c7ae24e6
source-git-commit: 6b8eecb3df0bb32344a5861a604a40402bb4d392
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---

# ACSD-55566: `mergeCart` 内部サーバーエラーでミューテーションが失敗する [!DNL GraphQL] response

ACSD-55566 パッチは、 `mergeCart` 内部サーバーエラーでミューテーションが失敗する [!DNL GraphQL] 応答。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.48 がインストールされています。 パッチ ID は ACSD-55566 です。 この問題はAdobe Commerce 2.5.0 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.6-p4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

`mergeCart` 内部サーバーエラーでミューテーションが失敗する [!DNL GraphQL] 同じバンドル項目を持つソースと宛先の買い物かごを結合する場合の応答。

<u>再現手順</u>:

1. カスタムソースとカスタム在庫を作成します。
1. 作成した在庫をメインの web サイトに割り当てます。
1. 単純な製品を作成し、それに作成したソース（qty=2）を割り当てます。
1. 1 つのオプションと 1 つの子製品（手順 3 で作成した製品）を持つバンドル製品を作成します。
1. 次を使用したゲスト用カートの作成 [!DNL GraphQL].
1. 両方のオプションが選択された状態でバンドル製品を追加します。
1. を保存します *cartID*.
1. 顧客を作成し、顧客トークンを生成します。
1. 顧客カートを作成します。
1. 同じ設定の同じバンドル製品を買い物かごに追加します。
1. ゲストの買い物かごを顧客の買い物かごに結合してみます。

<u>期待される結果</u>:

顧客の買い物かごには、両方の買い物かごからの製品が含まれています。

<u>実際の結果</u>:

内部エラーが発生します。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
