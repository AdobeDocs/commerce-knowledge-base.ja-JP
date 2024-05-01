---
title: 「ACSD-48813：属性の検索の重み付けに基づいた、関連性の高い結果が検索に表示されない」
description: ACSD-48813 パッチを適用すると、属性の検索重み付けに基づいて検索で関連する結果が表示されないAdobe Commerceの問題が修正されます。
exl-id: 089e3ab3-0dfa-4f81-85c7-f6060f326d97
feature: Admin Workspace, Attributes, Search
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# ACSD-48813：属性の検索重み付けに基づいた、関連性の高い結果が検索に表示されない

ACSD-48813 パッチにより、属性の検索重み付けに基づいて検索で関連する結果が表示されない問題が修正されました。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.29 がインストールされています。 パッチ ID は ACSD-48813 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

属性の検索の重み付けに基づいて、検索で関連する結果が表示されない。

<u>再現手順</u>:

1. サンプルデータを使用してAdobe Commerceをインストールします。
1. 検索エンジンをに設定 [!DNL Elasticsearch].
1. 管理者としてログインします。
1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Attributes]** > **[!UICONTROL Products]**.
1. を開きます *名前* 属性。
1. ストアフロントを開きます *[!UICONTROL Properties]* タブ。
1. を選択 [!UICONTROL Search Weight] = *10* ドロップダウン値から。
1. クリック **[!UICONTROL Save Attribute]**.
1. 次に、ストアフロントを開いて単語を検索します *戻る*.

<u>期待される結果</u>:

バックパック商品は検索結果の一番上に返されます。

<u>実際の結果</u>:

バックパック商品は、検索結果の途中で返されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
