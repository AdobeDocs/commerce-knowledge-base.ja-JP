---
title: 「ACSD-54007：顧客データの読み込み時の未定義の配列キー_scope エラー」
description: ACSD-54007 パッチを適用すると、カスタマーデータの読み込み時に未定義の配列キー_scope エラーが表示されるAdobe Commerceの問題を修正できます。
feature: Data Import/Export
role: Admin, Developer
exl-id: b14a14fd-5021-460f-8ca9-c9845859df97
source-git-commit: f12e25ac5dd607cc614dd99c90c5e104b2cee6a8
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# ACSD-54007：顧客データのインポート時に未定義の配列キー_scope エラーが発生しました

ACSD-54007 パッチは、が存在する問題を修正します。 *未定義の配列キー_scope* 顧客データの読み込みエラー。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.40 がインストールされています。 パッチ ID は ACSD-54007 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

顧客データをインポートすると、 *未定義の配列キー_scope* エラー。

<u>再現手順</u>:

1. Commerce管理者に移動します **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** >  **[!UICONTROL Import]**、設定 **[!UICONTROL Entity Type]** 対象： **[!UICONTROL Stock Sources]** をクリックして、ストックソースの csv ファイル（ソースコード、SKU、数量、ステータスを含む）を読み込みます。
1. 「顧客とアドレス」（単一ファイル）を選択し、顧客のアドレスの詳細を含む csv ファイルを読み込みます。

<u>期待される結果</u>:

エラーはありません。

<u>実際の結果</u>:

次のエラーが発生します。  *警告：84 行目の/var/www/html/vendor/magento/module-customer-import-export/Model/ResourceModel/Import/CustomerComposite/Data.phpに未定義の配列キー「_scope」*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
