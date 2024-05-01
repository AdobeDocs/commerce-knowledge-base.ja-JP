---
title: '''ACSD-49835: [!UICONTROL Use Default Value] チェックボックスが保存されていません」'
description: Adobe Commerce ACSD-49835 パッチを適用して、 [!UICONTROL Use Default Value] 複数選択属性のストアレベルでチェックボックスが正しく保存されない。
exl-id: 84270551-c8a9-4b08-a055-ffdcc538c33d
feature: Storefront
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---

# ACSD-49835: [!UICONTROL Use Default Value] チェックボックスが保存されていません

ACSD-49835 パッチは、 [!UICONTROL Use Default Value] 複数選択属性のストアレベルでチェックボックスが正しく保存されない。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.29 がインストールされています。 パッチ ID は ACSD-49835 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

この [!UICONTROL Use Default Value] 複数選択属性のストアレベルでチェックボックスが正しく保存されない。

<u>再現手順</u>:

1. を作成 **[!UICONTROL Multiple-select Attribute]** 。対象： **[!UICONTROL Stores]** > **[!UICONTROL Attributes]** > **[!UICONTROL Product]** 属性セットに追加します。
1. に移動 **[!UICONTROL Product]** と保存します **[!UICONTROL Values]** 。対象： **[!UICONTROL All Store Views (Default Scope)]**.
1. 特定のに移動 **[!UICONTROL Store View Scope]** 製品を保存します。
1. に移動 **[!UICONTROL Store View Scope]** を実行して、 **[!UICONTROL Use Default Value]** チェックボックス。

<u>期待される結果</u>:

をチェックすると、複数選択の属性値が適切に保存されます [!UICONTROL Use Default Value] のチェックボックス [!UICONTROL Store View Scope].

<u>実際の結果</u>:

をチェックすると、複数選択の属性値が正しく保存されない [!UICONTROL Use Default Value] のチェックボックス [!UICONTROL Store View Scope].

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
