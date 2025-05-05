---
title: 「ACSD-52143：製品の読み込み後にカスタムオプションが削除される」
description: ACSD-52143 パッチを適用して、製品の読み込み後にカスタマイズオプションが削除されるAdobe Commerceの問題を修正してください。
feature: Data Import/Export
role: Admin, Developer
exl-id: 7dde1efe-37a3-443f-9ce1-82cf1b3d9da7
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# ACSD-52143：製品の読み込み後にカスタムオプションが削除される

ACSD-52143 パッチは、製品の読み込み後にカスタムオプションが削除される問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.37 がインストールされている場合に使用できます。 パッチ ID は ACSD-52143 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p2

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カスタムオプションは、製品の読み込み後に削除されます。

<u> 再現手順 </u>:

1. **[!UICONTROL Store]**/**[!UICONTROL All Stores]** に移動し、マルチストアインスタンス（2 つのストア表示を持つ 1 つの web サイト）を設定します。
1. **[!UICONTROL Catalog]**/**[!UICONTROL Products]** に移動し、[!UICONTROL Customizable Options] で 2 つの製品を作成します。
1. 各製品に [!UICONTROL Customizable Option] を追加します。
1. 2 番目のストア表示に切り替えて、各製品の製品名を変更します。
1. **[!UICONTROL System]**/**[!UICONTROL Data Transfer]**/**[!UICONTROL Export]** に移動し、作成した 2 つの製品を書き出します。
1. CSV ファイルをダウンロードします。
1. **[!UICONTROL System]**/**[!UICONTROL Data Transfer]**/**[!UICONTROL Import]** に移動し、ファイルを再インポートします。
1. 両方の製品を確認します。

<u> 期待される結果 </u>:

製品の読み込み後に、カスタムオプションは削除されません。

<u> 実際の結果 </u>:

商品の読み込み後に税関オプションが削除されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
