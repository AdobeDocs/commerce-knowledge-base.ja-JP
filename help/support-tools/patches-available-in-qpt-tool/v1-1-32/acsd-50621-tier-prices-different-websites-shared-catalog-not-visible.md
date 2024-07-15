---
title: 「ACSD-50621：共有カタログ内の異なる web サイトの階層価格が表示されない」
description: 複数の web サイトを使用している場合、共有カタログ内の各 web サイトの階層価格が表示されないというAdobe Commerceの問題を修正するために、ACSD-50621 パッチを適用してください。
exl-id: 6d6635bc-4f76-4e2f-9bc7-0276cced8ca9
feature: Catalog Management, Orders
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# ACSD-50621：共有カタログ内の異なる web サイトの階層価格が表示されない

ACSD-50621 パッチは、複数の web サイト環境で編集する場合、共有カタログ内の様々な web サイトの階層価格が表示されない問題を修正しました。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.32 がインストールされている場合に使用できます。 パッチ ID は ACSD-50621 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

複数 web サイト環境で編集する場合、共有カタログ内の様々な web サイトの階層価格は表示されません。

<u> 再現手順 </u>:

1. **[!UICONTROL Catalog Price Scope]** を **[!UICONTROL Website]** に設定します。
1. 追加の web サイト、ストア、ストアレビューを作成します。
1. シンプルな製品を作成し、すべての web サイトに割り当てます。
1. カスタムの共有カタログを作成します。
1. 作成したカスタム共有カタログの **[!UICONTROL Set Pricing and Structure]** に移動します。
1. 手順 1：カタログ用の製品を選択します。 作成したシンプルな製品を追加します。
1. 手順 2：カスタム価格を設定し、**[!UICONTROL Configure]** をクリックします。
1. Web サイトごとに異なる階層価格を設定します。
1. 「**[!UICONTROL Done]**」を選択し、「**[!UICONTROL Generate Catalog]**」をクリックしてから「**[!UICONTROL Save]**」をクリックします。
1. cron を実行します。
1. **[!UICONTROL Set Pricing and Structure]**/**[!UICONTROL Configure]**/**[!UICONTROL Next]**/**[!UICONTROL Configure]** に移動し、階層価格を確認します。

<u> 期待される結果 </u>:

異なる web サイトに対して以前に設定されたすべての階層価格が存在します。

<u> 実際の結果 </u>:

以前に設定された階層価格は存在しません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
