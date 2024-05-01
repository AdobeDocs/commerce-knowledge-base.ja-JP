---
title: 「ACSD-56246：製品アップデートのスケジュールで、複数選択の属性値がクリアされる」
description: ACSD-56246 パッチを適用して、製品アップデートのスケジュールで複数選択属性値がクリアされるAdobe Commerceの問題を修正してください。
feature: Products, Attributes, Staging
role: Admin, Developer
exl-id: ddca8ac0-6aa8-4bf1-b8c2-4819758cb198
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# ACSD-56246：製品アップデートをスケジュールすると、複数選択の属性値がクリアされる

ACSD-56246 パッチでは、製品アップデートのスケジュールによって複数選択属性の値がクリアされる問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.44 がインストールされています。 パッチ ID は ACSD-56246 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

スケジュールされた製品アップデートにより、複数選択の属性値がクリアされます。

<u>再現手順</u>:

1. Adobe Commerceをインストールします。
1. に移動 **[!UICONTROL Admin]** > **[!UICONTROL Stores]** > **[!UICONTROL Attributes]** > **[!UICONTROL Product]** 次の属性を作成します。

   * デフォルトのラベル：プログラム
   * 店舗所有者のカタログ入力タイプ：複数選択
   * オプション （属性の値）の管理：Choice、Sunscape、Safetyshield
   * 属性コード：customer_program
   * 範囲：グローバル
   * 列に追加オプション：いいえ
   * フィルターオプションで使用：なし
   * ストアフロント プロパティ
   * 位置： *333*
   * ストアフロントでHTMLタグを許可：いいえ

1. 実行
   `bin/magento setup:perf:generate-fixtures setup/performance-toolkit/profiles/ce/small.xml`.
1. 実行
   `bin/magento setup:upgrade`.
1. に移動します **[!UICONTROL Admin]** > シンプルな製品を選択 > プログラム属性内のすべての項目を選択 > をクリック **[!UICONTROL Save the product]**.
1. 次分にこの製品のアップデートをスケジュールし、次のコマンドを実行してコンテンツのステージングを機能させます。
   `for i in {1..100}; do bin/magento cron:run; done`.

<u>期待される結果</u>:

商品 **[!UICONTROL program]** 属性は変更できません。

<u>実際の結果</u>:

商品 **[!UICONTROL program]** 属性がクリアされました。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
