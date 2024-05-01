---
title: 「ACSD-48262：次の場合、ストアフロントに製品が表示されない [!UICONTROL Allow All Products Per Page] 設定済み [!UICONTROL Yes]'
description: 次の場合に ACSD-48262 パッチを適用して、Adobe Commerceの問題を修正してください [!UICONTROL Allow All Products Per Page] はに設定されています。 [!UICONTROL Yes].
exl-id: 327cad03-441d-4adb-8a10-802f06d3fcd1
feature: Admin Workspace, Cache, Categories, Orders, Products, Storefront
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# ACSD-48262：次の場合、ストアフロントに製品が表示されない [!UICONTROL Allow All Products Per Page] 設定済み *[!UICONTROL Yes]*

ACSD-48262 パッチは、の場合にストアフロントに製品が表示されない問題を修正しました。 [!UICONTROL Allow All Products Per Page] はに設定されています。 *[!UICONTROL Yes]*. このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.25 がインストールされています。 パッチ ID は ACSD-48262 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） >=2.4.5 &lt; 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ACSD-48262 パッチは、の場合にストアフロントに製品が表示されない問題を修正しました。 [!UICONTROL Allow All Products Per Page] はに設定されています。 *[!UICONTROL Yes]*.

<u>再現手順</u>:

1. テストカテゴリを作成します。
1. テストカテゴリでテスト製品を作成します。
1. 製品を参照してストアフロントのカテゴリページをテストし、製品が表示されていることを確認します。
1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** を設定して、 [!UICONTROL Allow All Products Per Page] をに設定しています *[!UICONTROL Yes]*.
1. キャッシュをクリアします。
1. ストアフロントのカテゴリページをご確認ください。

<u>期待される結果</u>:

商品が表示されます。

<u>実際の結果</u>:

商品が表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。


## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
