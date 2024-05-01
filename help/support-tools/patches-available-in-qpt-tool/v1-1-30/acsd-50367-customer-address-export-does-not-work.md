---
title: 「ACSD-50367：顧客アドレスのエクスポートが複数選択属性で機能しない」
description: 値のない複数選択**ーザーの顧客アドレス属性が作成された場合に、顧客アドレスの書き出しが機能しないAdobe Commerceの問題を修正するため**ACSD-50367 パッチを適用します。
exl-id: 688831d4-b49e-48fa-b4db-1328cda09a2b
feature: Admin Workspace, Attributes, Data Import/Export, Shipping/Delivery
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# ACSD-50367：顧客アドレスのエクスポートが機能しない

ACSD-50367 パッチは、複数選択したときに顧客アドレスの書き出しが機能しない問題を修正します **`Customer Address`** 値のない属性が作成されます。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.30 がインストールされています。 パッチ ID は ACSD-50367 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

複数選択の場合、顧客アドレスのエクスポートが機能しない **`Customer Address`** 値のない属性が作成されます。

<u>前提条件</u>:

住所を持つ顧客を作成します。

<u>再現手順</u>:

1. 複数選択の作成 **`Customer Address`** 属性： **[!UICONTROL Admin]** > **[!UICONTROL Stores]** > **[!UICONTROL Customer Addresses]**.
1. に移動 **[!UICONTROL Admin]** > **[!UICONTROL System]** > **[!UICONTROL Export]**&#x200B;を選択し、 **`Customer Address`** エンティティタイプ。
1. 顧客アドレスをエクスポートします。 何も書き出されていないことがわかります。
1. 複数選択の削除 **`Customer Address`** 属性を設定し、顧客アドレスを再度書き出します。 今回は、アドレスの CSV ファイルが生成されます。

<u>期待される結果</u>:

顧客アドレスは、複数選択の際に CSV ファイルとしてエクスポートできます **`Customer Address`** 属性が作成されます。

<u>実際の結果</u>:

複数選択の場合、顧客アドレスを CSV ファイルとして書き出すことはできません **`Customer Address`** 属性が作成されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
