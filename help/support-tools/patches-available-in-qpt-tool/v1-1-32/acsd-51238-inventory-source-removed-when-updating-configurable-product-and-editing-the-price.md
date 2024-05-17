---
title: 「ACSD-51238：設定可能な製品を更新して価格を編集すると、在庫ソースが削除される」
description: 設定可能な商品をアップデートして価格を編集する際に、在庫ソースが削除されるAdobe Commerceの問題を修正するために、ACSD-51238 パッチを適用してください。
exl-id: ab2f60fd-5da3-45f7-a489-6f4f9d34e1f1
feature: Configuration, Inventory, Orders, Products
role: Admin
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# ACSD-51238：設定可能な製品を更新して価格を編集すると、在庫ソースが削除される

ACSD-51238 パッチは、設定可能な製品を更新して価格を編集する際に在庫ソースが削除される問題を修正します。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.32 がインストールされています。 パッチ ID は ACSD-51238 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

設定可能な商品を更新し、価格を編集すると、在庫ソースが削除されます。

<u>再現手順</u>:

1. インストール **[!DNL Adobe Commerce]** （を使用） **[!DNL Inventory module]**
1. に移動します **[!UICONTROL Admin]** -> **[!UICONTROL Stores]** -> **[!UICONTROL Inventory]** および作成 *2 つのソース* および *二株*.
1. を作成 **[!UICONTROL configurable product]** そしてそれを割り当て先： **[!UICONTROL default sources]** または **[!UICONTROL newly created sources]**.
1. 「」をクリック **[!UICONTROL next button]** および *保存* 商品。
1. 同じものを編集する **[!UICONTROL Configurable Product]** をクリックし、 **[!UICONTROL Edit Configuration]** 内 **[!UICONTROL Configuration tab]**.
1. 対象： `Step 3: Bulk Images,Price and Quantity`、を変更します `price` と終了します `Quantity` および `Images` 対象： `Skip quantity at this time` および `Skip image uploading at this time` それぞれ。
1. クリックする **[!UICONTROL next button]** 製品を生成します。

<u>期待される結果</u>

内のソースごとの数量 **[!UICONTROL Configuration tab]** 空にはしないでください。

<u>実際の結果</u>

内のソースごとの数量 **[!UICONTROL Configuration tab]** が空である。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
