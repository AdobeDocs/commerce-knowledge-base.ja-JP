---
title: 「ACSD-48313：属性値 [!UICONTROL configurable_variations] コンマが含まれている場合、列は解析されません」
description: 属性値にコンマが含まれている場合、[!UICONTROL configurable_variations] 列が解析されないAdobe Commerceの問題を修正するために、ACSD-48313 パッチを適用してください。
exl-id: 0ac3f8da-4da3-4308-bea4-98a5b6926b0d
feature: Attributes, Configuration
role: Admin
source-git-commit: 4cb43c4f16238253fc7fc75d9af9b921dfa74158
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# ACSD-48313：属性値 **[!UICONTROL configurable_variations]** コンマが含まれている場合、列は解析されません

ACSD-48313 パッチは、属性値にコンマが含まれ **[!UICONTROL configurable_variations]** いる場合に列が解析されない問題を解決します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.25 がインストールされている場合に使用できます。 パッチ ID は ACSD-48313 です。 この問題が修正されるバージョンは、まだ利用できません。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.4-p5

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

設定可能な製品を書き出した後は、**[!UICONTROL configurable_variations]** 属性のフォーマットに問題があるので、結果のファイルを再度インポートすることはできません。 これは、コンマを含む属性オプションがある場合に発生します。

<u> 再現手順 </u>:

1. **[!UICONTROL Stores]**/**[!UICONTROL Attributes]**/**[!UICONTROL Product]** に移動し、新しい属性 _サイズ_ を作成します。
1. ストア所有者のカタログ入力タイプ：**[!UICONTROL Dropdown]**。
1. コンマを含むオプションを作成（例：）。
   * 10,2cm
   * 15,5cm
1. **[!UICONTROL Advanced Attribute Properties]** - スコープ：_グローバル_。
1. 設定の作成機能を使用して、新しい設定可能な製品を作成します。
1. 上記の属性 _Size_ と、コンマを含む 2 つのオプションを選択します。
1. **[!UICONTROL System]**/**[!UICONTROL Data Transfer]**/**[!UICONTROL Export]** に移動して、新しい Products export を作成します（cron を実行して CSV ファイルの生成をトリガーします）。
1. **[!UICONTROL System]**/**[!UICONTROL Data Transfer]**/**[!UICONTROL Import]** に移動し、上記で作成したのと同じ CSV ファイルを再読み込みします。

<u> 期待される結果 </u>:

ユーザーはファイルを読み込めるはずです。

<u> 実際の結果 </u>:

```
1. Column configurable_variations: Attribute with code "2cm" does not exist or is missing from product attribute set in row(s): 3
2. Column configurable_variations: Attribute with code "5cm" does not exist or is missing from product attribute set in row(s): 3
3. Column configurable_variations: Invalid option value for attribute "size" in row(s): 3
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
