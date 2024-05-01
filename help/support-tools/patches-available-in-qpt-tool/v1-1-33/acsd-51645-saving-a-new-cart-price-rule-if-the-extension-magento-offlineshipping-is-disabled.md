---
title: 「ACSD-51645:Magentoextension_OfflineShipping が無効な場合の、新しい買い物かご価格ルールの保存」
description: Magento拡張機能 extension_OfflineShipping が無効になっている場合、新しい買い物かご価格ルールを保存するとエラーが発生するAdobe Commerceの問題を修正するために ACSD-51645 パッチを適用してください。
exl-id: 301086bb-7aab-4e74-93e6-9080eebcb026
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# ACSD-51645:Magentoextension_OfflineShipping が無効な場合の、新しい買い物かご価格ルールの保存

ACSD-51645 パッチでは、Magentoextension_OfflineShipping が無効になっている場合に、新しい買い物かご価格ルールを保存するとエラーが発生する問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.33 がインストールされています。 パッチ ID は ACSD-51645 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

拡張機能の場合、新しい買い物かご価格ルールを保存するとエラーが発生する `Magento_OfflineShipping` が無効になっています。

<u>再現手順</u>:

1. を無効にする `Magento_OfflineShipping` モジュール。
1. へのログイン **Admin**.
1. に移動 **[!UICONTROL Marketing]** > **[!UICONTROL Cart Price Rules]**.
1. 新しいを作成 **[!UICONTROL Cart Price Rule]**.
1. 必須フィールドに入力します。
1. を保存します **[!UICONTROL Cart Price Rule]**.

<u>期待される結果</u>:

買い物かご価格ルールが正常に保存されました。

<u>実際の結果</u>:

次のエラーが発生します。
`report.ERROR: Warning: Undefined array key "simple_free_shipping" in app/code/Magento/SalesRule/Controller/Adminhtml/Promo/Quote/Save.php on line 67 [] []`

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
