---
title: 「ACSD-48212：製品の読み込みによって製品が間違ったソースに割り当てられる」
description: 製品の読み込みによって製品が誤ったソースに割り当てられるAdobe Commerceの問題を修正するには、ACSD-48212 パッチを適用してください。
exl-id: b3426f62-f73a-4b76-8e0e-544a9133720f
feature: Admin Workspace, Data Import/Export, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# ACSD-48212：製品のインポートによって製品が誤ったソースに割り当てられる

ACSD-48212 パッチは、製品の読み込みによって製品が誤ったソースに割り当てられる問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.26 がインストールされています。 パッチ ID は ACSD-48212 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品の読み込みによって、製品が誤ったソースに割り当てられる。

<u>再現手順</u>:

1. サブ在庫ソースを作成します。
1. デフォルトの在庫ソースのみを持つ製品を作成します。
1. 商品を書き出します。
1. 実行 `bin/magento cron:run`.
1. 開く **[!UICONTROL Catalog]** > **[!UICONTROL Prdoucts]**.
1. グリッドから製品を選択します。
1. を使用して在庫を割り当て解除 *[!UICONTROL mass action]* メニュー。
1. 実行 `bin/magento cron:run`.
1. を使用してセカンダリソースを割り当てます *[!UICONTROL mass action]* メニュー。
1. 実行 `bin/magento cron:run`.
1. を使用した製品の削除 *[!UICONTROL mass action]* メニュー。
1. 実行 `bin/magento cron:run`.
1. 以前に書き出した CSV を使用して製品を読み込みます。
1. ソース割り当てを確認します。

<u>期待される結果</u>:

製品は、デフォルトソースにのみ割り当てられます。

<u>実際の結果</u>:

製品は、デフォルトとセカンダリの両方のソースに割り当てられます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
