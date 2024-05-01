---
title: 「ACSD-47079：サブ製品の在庫ステータスが変更された場合、複合製品の在庫ステータスが更新されない」
description: ACSD-47079 パッチを適用すると、REST API POST /rest/V1/inventory/source-items を介してサブプロダクトのストックステータスが変更された場合に、複合プロダクト（バンドル、グループ化、設定可能）のストックステータスが更新されないAdobe Commerceの問題が修正されます。
exl-id: 603e4548-fb04-43b4-a033-4f2c7f665fae
feature: Orders, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# ACSD-47079：サブ製品の在庫ステータスが変更された場合、複合製品の在庫ステータスが更新されない

ACSD-47079 パッチでは、REST APIPOSTでサブプロダクトのストックステータスが変更された場合に、複合プロダクトのストックステータス（バンドル、グループ化、設定可能）が更新されない問題が修正されています `/rest/V1/inventory/source-items`. このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.24 がインストールされています。 パッチ ID は ACSD-47079 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.4-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

サブプロダクトのストックステータスが REST APIPOSTによって変更された場合、複合プロダクトのストックステータス（バンドル、グループ化、設定可能）は更新されません `/rest/V1/inventory/source-items`.

<u>再現手順</u>:

1. 設定可能でバンドルされた、グループ化された製品を、それぞれに 1 つのシンプルな子製品で作成します。
1. 各子製品のシンプルなステータスをに設定します。 **[!UICONTROL Out of Stock]** の使用 `source-items` API 呼び出し。
1. 次に、親製品の在庫ステータスを確認します。

<u>期待される結果</u>:

親製品のステータスは「」です [!UICONTROL Out of Stock].

<u>実際の結果</u>:

親製品のステータスは「」です [!UICONTROL In Stock].

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
