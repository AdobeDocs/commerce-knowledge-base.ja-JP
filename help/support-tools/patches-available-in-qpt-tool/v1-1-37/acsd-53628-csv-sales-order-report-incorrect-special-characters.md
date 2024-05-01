---
title: 「ACSD-53628:CSV 販売注文レポートに間違った特殊文字が表示される」
description: ACSD-53628 パッチを適用すると、CSV 販売注文レポートに間違った特殊文字が表示されるAdobe Commerceの問題を修正できます。
feature: Orders, Data Import/Export
role: Admin, Developer
exl-id: d898fdb8-cab9-49ab-ad8e-43feadf49aa0
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# ACSD-53628:CSV 販売注文レポートに間違った特殊文字が表示される

ACSD-53628 パッチでは、CSV 販売注文レポートに間違った特殊文字が表示される問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.37 がインストールされています。 パッチ ID は ACSD-53628 です。 この問題はAdobe Commerce 2.4.7 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法）:2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法）:2.3.7～2.4.6-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

CSV 販売注文レポートに間違った特殊文字が表示される。

<u>再現手順</u>:

1. 変更 **[!UICONTROL Base Currency]** および **[!UICONTROL Default Display Currency]** 通貨の設定でユーロに変換します。
1. 注文します。
1. 管理サイドバーで、に移動します。 **[!UICONTROL Reports]** > **[!UICONTROL Sales]** > **[!UICONTROL Orders]**.
1. 日付を選択します。 クリック **[!UICONTROL Show Report]**. クリック **[!UICONTROL Export]** CSV を書き出します。

<u>期待される結果</u>:

書き出された CSV ファイル内の特殊文字は Excel で正しく表示されます。

<u>実際の結果</u>:

CSV 販売注文レポートで、特殊文字が正しく表示されません。


## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
