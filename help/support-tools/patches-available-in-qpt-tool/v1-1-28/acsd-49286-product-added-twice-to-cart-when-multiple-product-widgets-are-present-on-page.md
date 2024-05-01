---
title: 「ACSD-49286：複数の製品ウィジェットが存在する場合に、買い物かごに製品が 2 回追加される」
description: ページ上に複数の商品ウィジェットが存在する場合に、商品が買い物かごに 2 回追加されるAdobe Commerceの問題を修正するために、ACSD-49286 パッチを適用します。
exl-id: b1764943-945d-4ef9-9bbe-3f3c8383b5b1
feature: Admin Workspace, Orders, Products, Shopping Cart
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# ACSD-49286：複数の製品ウィジェットが存在する場合に、買い物かごに製品が 2 回追加される

ACSD-49286 パッチは、ページに複数の製品ウィジェットが存在する場合に、製品が買い物かごに 2 回追加される問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.28 がインストールされています。 パッチ ID は ACSD-49286 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ページに複数の製品ウィジェットが存在する場合、製品は買い物かごに 2 回追加されます。

<u>再現手順</u>:

1. 管理者にログインし、に移動します。 **[!UICONTROL Admin]** > **[!UICONTROL Content]** > **[!UICONTROL Page]** > **[!UICONTROL Home Page]**
1. 「コンテンツ」セクションで、をクリックします。 **[!UICONTROL Edit]** 使用 [!DNL Page Builder].
1. に 2 つの行要素を追加 **[!UICONTROL Content]**.
1. 製品を両方の行要素に追加します。
1. 最初の行で、製品の外観を [!UICONTROL Product Grid] 表示するカテゴリを選択します。
1. 2 行目で、製品の外観を [!UICONTROL Product Carousel] 表示するその他のカテゴリを選択します。
1. ストアフロントに移動 **[!UICONTROL Home Page]**&#x200B;製品グリッドから 1 つの製品を追加します。
1. から別の製品を追加 [!UICONTROL Product Carousel].

<u>期待される結果</u>:

から商品を買い物かごに追加した後で、製品数量を倍増しないでください [!UICONTROL Product Grid].

<u>実際の結果</u>:

から商品を買い物かごに追加すると、製品数が倍増します [!UICONTROL Product Grid].

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。 

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
