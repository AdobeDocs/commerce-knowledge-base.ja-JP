---
title: 'ACSD-53636：通常価格が表示されない [!UICONTROL Product Listing] ページ'
description: ACSD-53636 パッチを適用して、に通常の価格が表示されないAdobe Commerceの問題を修正してください*[!UICONTROL Product Listing]*特別価格の子製品を持つ設定可能な製品のページ。
feature: Catalog Management, Products
role: Admin, Developer
exl-id: 97b4eb64-92d1-4db1-8e5b-915b16115663
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# ACSD-53636：通常価格が表示されない *[!UICONTROL Product Listing]* ページ

ACSD-53636 パッチは、通常の価格がに表示されない問題を修正します *[!UICONTROL Product Listing]* 特別価格の子製品を持つ設定可能な製品のページ。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.43 がインストールされています。 パッチ ID は ACSD-53636 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.4-p6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

通常価格はに表示されません *[!UICONTROL Product Listing]* 特別価格の子製品を持つ設定可能な製品のページ。

<u>再現手順</u>:

1. 管理者にログインし、に移動します。 **[!UICONTROL Admin]** > **[!UICONTROL Catalog]**&#x200B;を選択し、設定可能な製品を作成するか開きます。
2. 子製品を開き、すべてまたは 1 つの子製品に特別価格を追加して、製品を保存します。
3. フロントエンドに移動し、 **[!UICONTROL Product Detail]** 設定可能な製品のページ。特別価格の子製品のスウォッチには、が表示されます。 *[!UICONTROL Regular price]* ストライクアウト（想定）。
4. フロントエンドに移動し、 **[!UICONTROL Product Listing]** 特別価格の設定可能な製品のページ。設定可能な製品スウォッチの変更には、 *[!UICONTROL Product Detail Page]* その他のシンプルな製品。

<u>期待される結果</u>:

日 *[!UICONTROL Product Listing]* 設定可能な製品ページには、子製品の通常の価格が表示されます。

<u>実際の結果</u>:

日 *[!UICONTROL Product Listing]* ページが開き、設定可能な製品に子製品の通常の価格が表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
