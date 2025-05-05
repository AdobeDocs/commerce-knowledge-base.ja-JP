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

ACSD-56246 パッチでは、製品アップデートのスケジュールによって複数選択属性の値がクリアされる問題が修正されています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.44 がインストールされている場合に使用できます。 パッチ ID は ACSD-56246 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

スケジュールされた製品アップデートにより、複数選択の属性値がクリアされます。

<u> 再現手順 </u>:

1. Adobe Commerceをインストールします。
1. **[!UICONTROL Admin]**/**[!UICONTROL Stores]**/**[!UICONTROL Attributes]**/**[!UICONTROL Product]** に移動し、次の属性を作成します。

   * デフォルトのラベル：プログラム
   * 店舗所有者のカタログ入力タイプ：複数選択
   * オプション （属性の値）の管理：Choice、Sunscape、Safetyshield
   * 属性コード：customer_program
   * 範囲：グローバル
   * 列に追加オプション：いいえ
   * フィルターオプションで使用：なし
   * ストアフロント プロパティ
   * 位置：*333*
   * ストアフロントでHTMLタグを許可：いいえ

1. 実行
   `bin/magento setup:perf:generate-fixtures setup/performance-toolkit/profiles/ce/small.xml`。
1. 実行
   `bin/magento setup:upgrade`。
1. **[!UICONTROL Admin]** / シンプルな製品を選択/ プログラム属性のすべての項目を選択/**[!UICONTROL Save the product]** をクリックに移動します。
1. 次分にこの製品のアップデートをスケジュールし、次のコマンドを実行してコンテンツのステージングを機能させます。
   `for i in {1..100}; do bin/magento cron:run; done`。

<u> 期待される結果 </u>:

製品の **[!UICONTROL program]** 属性は変更しないでください。

<u> 実際の結果 </u>:

製品の **[!UICONTROL program]** 属性がクリアされます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
