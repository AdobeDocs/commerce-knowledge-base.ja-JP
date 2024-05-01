---
title: 「ACSD-47803：在庫切れの設定可能な製品スウォッチが使用可能として表示される」
description: ACSD-47803 パッチを適用して、在庫切れの設定可能な商品スウォッチが使用可能と表示されるAdobe Commerceの問題を修正してください。
exl-id: 28b3f378-a790-4af6-9627-5bd8571523fd
feature: Configuration, Orders, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# ACSD-47803：在庫切れの設定可能な製品スウォッチが使用可能として表示される

ACSD-47803 パッチでは、在庫切れの設定可能な製品スウォッチが使用可能と表示される問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.24 がインストールされています。 パッチ ID は ACSD-47803 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

在庫切れの設定可能な製品スウォッチが使用可能として表示されます。

<u>再現手順</u>:

>[!NOTE]
>
>以下の手順は、サンプルデータを例として参照します。

1. が含まれる [!UICONTROL Commerce] 管理者、に移動します **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Inventory]** > **[!UICONTROL Stock Options]** を設定して、 **[!UICONTROL Display Out of Stock Products]** 対象： *はい*.
1. 再び、管理者から、に移動します。 **[!UICONTROL Catalog]** > **[!UICONTROL Products]** 製品編集ページで設定可能な製品を編集します（例えば、サンプルデータを使用している場合は「WB04」 SKU）。
   * 設定のバリエーションの 1 つに対して、量をに設定します *0* （例：「WB04-M-Purple」）。
1. 次に、ストアフロントで設定可能な製品を開きます。
1. 在庫が 0 の設定可能なバリアント（つまり「M」）の製品サイズを選択します。

<u>期待される結果</u>:

在庫切れオプションは無効になり、としてマークされます。 [!UICONTROL Out of Stock].

<u>実際の結果</u>:

すべてのカラースウォッチが有効になります（ [!UICONTROL Out of Stock].

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
