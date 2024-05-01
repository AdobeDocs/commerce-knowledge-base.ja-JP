---
title: '''ACSD-48313: [!UICONTROL configurable_variations] 属性値にコンマが含まれる場合、列は解析されません。'
description: Adobe Commerce ACSD-48313 パッチを適用して、 [!UICONTROL configurable_variations] 属性値にコンマが含まれる場合、列は解析されません。
exl-id: 0ac3f8da-4da3-4308-bea4-98a5b6926b0d
feature: Attributes, Configuration
role: Admin
source-git-commit: 4cb43c4f16238253fc7fc75d9af9b921dfa74158
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# ACSD-48313: **[!UICONTROL configurable_variations]** 属性値にコンマが含まれる場合、列は解析されません

ACSD-48313 パッチは、次の問題を解決します。 **[!UICONTROL configurable_variations]** 属性値にコンマが含まれる場合、列は解析されません。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.25 がインストールされています。 パッチ ID は ACSD-48313 です。 この問題が修正されるバージョンは、まだ利用できません。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.4-p5

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

設定可能な製品を書き出した後は、のフォーマットに問題があるので、結果のファイルを再度インポートすることはできません。 **[!UICONTROL configurable_variations]** 属性。 これは、コンマを含む属性オプションがある場合に発生します。

<u>再現手順</u>:

1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Attributes]** > **[!UICONTROL Product]** および新しい属性の作成 _サイズ_:
1. ストア所有者のカタログ入力タイプ： **[!UICONTROL Dropdown]**.
1. コンマを含むオプションを作成（例：）。
   * 10,2cm
   * 15,5cm
1. **[!UICONTROL Advanced Attribute Properties]**  – 範囲： _グローバル_.
1. 設定の作成機能を使用して、新しい設定可能な製品を作成します。
1. 上記の属性を選択します。 _サイズ_ コンマを含む 2 つのオプション
1. に移動 **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Export]** を作成して、新しい商品のエクスポートを作成します（cron を実行して CSV ファイルの生成をトリガーします）。
1. に移動 **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Import]** そして、上記で作成したのと同じ CSV ファイルを再度読み込んでみます。

<u>期待される結果</u>:

ユーザーはファイルを読み込めるはずです。

<u>実際の結果</u>:

```
1. Column configurable_variations: Attribute with code "2cm" does not exist or is missing from product attribute set in row(s): 3
2. Column configurable_variations: Attribute with code "5cm" does not exist or is missing from product attribute set in row(s): 3
3. Column configurable_variations: Invalid option value for attribute "size" in row(s): 3
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。


## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
