---
title: 「ACSD-50621：共有カタログ内の異なる web サイトの階層価格が表示されない」
description: 複数の web サイトを使用している場合、共有カタログ内の各 web サイトの階層価格が表示されないというAdobe Commerceの問題を修正するために、ACSD-50621 パッチを適用してください。
exl-id: 6d6635bc-4f76-4e2f-9bc7-0276cced8ca9
feature: Catalog Management, Orders
role: Admin
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# ACSD-50621：共有カタログ内の異なる web サイトの階層価格が表示されない

ACSD-50621 パッチは、複数の web サイト環境で編集する場合、共有カタログ内の様々な web サイトの階層価格が表示されない問題を修正しました。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.32 がインストールされています。 パッチ ID は ACSD-50621 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

複数 web サイト環境で編集する場合、共有カタログ内の様々な web サイトの階層価格は表示されません。

<u>再現手順</u>:

1. を **[!UICONTROL Catalog Price Scope]** 対象： **[!UICONTROL Website]**.
1. 追加の web サイト、ストア、ストアレビューを作成します。
1. シンプルな製品を作成し、すべての web サイトに割り当てます。
1. カスタムの共有カタログを作成します。
1. に移動 **[!UICONTROL Set Pricing and Structure]** を作成したカスタム共有カタログ用に設定します。
1. 手順 1：カタログ用の製品を選択します。 作成したシンプルな製品を追加します。
1. 手順 2：カスタム価格を設定し、をクリックする **[!UICONTROL Configure]**.
1. Web サイトごとに異なる階層価格を設定します。
1. を選択 **[!UICONTROL Done]** をクリックし、 **[!UICONTROL Generate Catalog]** 次に、をクリックします **[!UICONTROL Save]**.
1. cron を実行します。
1. に移動します。 **[!UICONTROL Set Pricing and Structure]** > **[!UICONTROL Configure]** > **[!UICONTROL Next]** > **[!UICONTROL Configure]** 階層の価格を確認します。

<u>期待される結果</u>:

異なる web サイトに対して以前に設定されたすべての階層価格が存在します。

<u>実際の結果</u>:

以前に設定された階層価格は存在しません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
