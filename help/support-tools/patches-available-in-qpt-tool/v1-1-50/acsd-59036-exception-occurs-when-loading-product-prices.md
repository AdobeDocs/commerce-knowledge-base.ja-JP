---
title: 「ACSD-59036：下限と上限の両方が$0 に設定された製品価格を読み込むと、例外が発生します」
description: ACSD-59036 パッチを適用すると、下限と上限の両方が*$0*に設定された商品価格を読み込む際に例外が発生するAdobe Commerceの問題を修正できます。
feature: Categories, Products, Storefront, Search
role: Admin, Developer
source-git-commit: d711fb8ff8876a4a514daade6d7df4d7cf7e3593
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---


# ACSD-59036：下限と上限の両方が *$0 に設定された製品価格を読み込むと、例外が発生します*

ACSD-59036 パッチは、下限と上限の両方が *$0* に設定された製品価格を読み込む際に例外が発生する問題を修正しました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.50 がインストールされている場合に使用できます。 パッチ ID は ACSD-59036 です。 この問題はAdobe Commerce 2.4.8 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.4.7

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.4.7 ～ 2.4.7-p2

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

下限と上限の両方が *$0* に設定された製品価格を読み込むと、例外が発生します。

この問題は、価格範囲を含むクエリを読み込む際に、アルゴリズムが NULL 値を考慮しないために発生しています。 これを修正するには、下限と上限の両方の範囲が NULL かどうかを確認し、NULL の場合は、両方の制限に *0* の値を割り当てます。 これにより、エラーがスローされるのを防ぐことができます。

<u> 再現手順 </u>:

1. *13* のシンプルな製品を作成します。
1. すべての *13* 製品を 1 つのカテゴリに割り当てます。
1. 1 つの製品の価格を 1322.94 *ド* に設定してください。
1. その他の商品はすべて 0 *ド* に設定してください。
1. [!DNL OpenSearch] を検索エンジンとして設定します。
1. **[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Catalog]**/**[!UICONTROL Storefront]** に移動し、**[!UICONTROL PLP]** のカウントを *16* に設定します。
1. **[!UICONTROL Price Navigation Step Calculation]** を *自動（製品数を平均化）* に設定します。
1. 完全な再インデックスを実行します。
1. *[!UICONTROL Category]* ページを開きます。

<u> 期待される結果 </u>:

*[!UICONTROL Category]* のページには、すべての製品が表示されます。

<u> 実際の結果 </u>:

エラーが発生しました：

```JSON
report.CRITICAL: OpenSearch\Common\Exceptions\BadRequest400Exception: {"error":{"root_cause":[{"type":"x_content_parse_exception","reason":"[1:193] [bool] failed to parse field [must]"}],"type":"x_content_parse_exception","reason":"[1:193] [bool] failed to parse field [filter]","caused_by":{"type":"x_content_parse_exception","reason":"[1:193] [bool] failed to parse field [must]","caused_by":{"type":"illegal_argument_exception","reason":"field name is null or empty"}}},"status":400} in /vendor/opensearch-project/opensearch-php/src/OpenSearch/Connections/Connection.php:664
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
