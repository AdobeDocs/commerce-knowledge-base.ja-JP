---
title: 「ACSD-55238：空の製品メタ説明の保存」
description: によって生成されたHTMLコードを含む製品説明がAdobe Commerceで生成される問題を修正するために、ACSD-55238 パッチを適用します。 [!DNL Page Builder] または、常にメタ記述に別のHTMLエディタが表示され、空に設定することはできません。
feature: Products, Page Builder, Page Content
role: Admin, Developer
exl-id: 250026c3-925d-4a62-9855-d892c86d3d24
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# ACSD-55238：空の製品メタ説明の保存

ACSD-55238 パッチは、HTMLエディタによって生成されたHTMLコードを含む製品説明が常にメタ説明に表示される問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.42 がインストールされています。 パッチ ID は ACSD-55238 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

によって生成されたHTMLコードを含む商品説明 [!DNL Page Builder] または、常にメタ記述に別のHTMLエディタが表示され、空に設定することはできません。

<u>再現手順</u>:

1. に移動 **[!UICONTROL Admin]** > **[!UICONTROL Content]** > **[!UICONTROL Block]** 任意のコンテンツを含む新しいブロックを作成します。
1. に移動 **[!UICONTROL Admin]** > **[!UICONTROL Catalog]** > **[!UICONTROL Product]** 新しい製品を作成します。 メタの説明を空に設定します。
1. 上記で作成したブロックを次を使用して追加 *[!DNL Page Builder]* が含まれる *[!UICONTROL Content]* タブをクリックして、商品を保存します。
1. ストアフロントで製品を開き、doc 要素を確認します `meta name = "description"`.

<u>期待される結果</u>:

メタ説明が空です。

<u>実際の結果</u>:

製品の説明にブロックが含まれている場合、製品のメタ説明に使用されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
