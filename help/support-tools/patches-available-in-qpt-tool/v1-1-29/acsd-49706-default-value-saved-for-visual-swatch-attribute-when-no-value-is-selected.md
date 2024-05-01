---
title: 「ACSD-49706：値が選択されていない場合にビジュアルスウォッチ属性に対して保存されるデフォルト値」
description: 値が選択されていない場合にビジュアルスウォッチ属性のデフォルト値が保存されるAdobe Commerceの問題を修正するために、ACSD-49706 パッチを適用します。
exl-id: fe6071df-f2a4-443a-acfa-67f3d253c5e4
feature: Admin Workspace, Attributes
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# ACSD-49706：値が選択されていない場合にビジュアルスウォッチ属性に対して保存されるデフォルト値

ACSD-49706 パッチでは、値が選択されていないときに視覚的スウォッチ属性のデフォルト値が保存される問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.29 がインストールされています。 パッチ ID は ACSD-49706 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

値が選択されていない場合、ビジュアルスウォッチ属性のデフォルト値が保存されます。

<u>再現手順</u>:

1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Attributes]** > **[!UICONTROL Product]**.
1. クリック **[!UICONTROL Add New Attribute]**.
1. フィールドに入力します。

   * たとえば、入力タイプを選択します *[!UICONTROL Visual Swatch]*、複数のオプションを追加します（など） *赤*, *緑*）に設定します。 必ず、これらのオプションのいずれかをデフォルトとして選択してください。
   * クリック **[!UICONTROL Save Attribute]**.

1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Attributes]** > **[!UICONTROL Attribute Set]**.
1. を編集する *[!UICONTROL Default]* 属性セット。
1. 移動 *[!UICONTROL New Attribute]* 列から *[!UICONTROL Unassigned Attributes]* に *[!UICONTROL Product Details]* 中央の列のフォルダー。

   * クリック **[!UICONTROL Save]**.

1. を使用した新しい製品の作成 *[!UICONTROL Default]* 属性セット。

   * を残す *[!UICONTROL New Attribute]* 空にして保存します。

1. 保存すると、値がに表示されます。 *[!UICONTROL New Attribute]*.

<u>期待される結果</u>:

値が割り当てられていません *[!UICONTROL New Attribute]* デフォルトでは。

<u>実際の結果</u>:

製品を保存すると、デフォルト値が属性に適用されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
