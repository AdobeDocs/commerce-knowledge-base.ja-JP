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

ACSD-49706 パッチでは、値が選択されていないときに視覚的スウォッチ属性のデフォルト値が保存される問題が修正されています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.29 がインストールされている場合に使用できます。 パッチ ID は ACSD-49706 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

値が選択されていない場合、ビジュアルスウォッチ属性のデフォルト値が保存されます。

<u> 再現手順 </u>:

1. **[!UICONTROL Stores]**/**[!UICONTROL Attributes]**/**[!UICONTROL Product]** に移動します。
1. 「**[!UICONTROL Add New Attribute]**」をクリックします。
1. フィールドに入力します。

   * 例えば、入力タイプ *[!UICONTROL Visual Swatch]* を選択し、複数のオプション（*赤*、*緑* など）を追加します。 必ず、これらのオプションのいずれかをデフォルトとして選択してください。
   * 「**[!UICONTROL Save Attribute]**」をクリックします。

1. **[!UICONTROL Stores]**/**[!UICONTROL Attributes]**/**[!UICONTROL Attribute Set]** に移動します。
1. *[!UICONTROL Default]* 属性セットを編集します。
1. 列 *[!UICONTROL Unassigned Attributes]* の *[!UICONTROL New Attribute]* を中央の列の *[!UICONTROL Product Details]* フォルダーに移動します。

   * 「**[!UICONTROL Save]**」をクリックします。

1. *[!UICONTROL Default]* 属性セットを使用して新しい製品を作成します。

   * *[!UICONTROL New Attribute]* は空のままにして保存します。

1. 保存すると、値が *[!UICONTROL New Attribute]* に表示されます。

<u> 期待される結果 </u>:

デフォルトでは、*[!UICONTROL New Attribute]* に値は割り当てられていません。

<u> 実際の結果 </u>:

製品を保存すると、デフォルト値が属性に適用されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
