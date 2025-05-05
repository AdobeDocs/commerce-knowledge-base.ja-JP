---
title: 「ACSD-52929：デフォルトのソース項目の再インデックスに対する冗長リクエスト」
description: インベントリインデクサーが非同期モードで設定されている場合、デフォルトのソース項目を再インデックスする冗長なリクエストが発生するAdobe Commerceの問題を修正するために、ACSD-52929 パッチを適用してください。
feature: Configuration, Inventory
role: Admin, Developer
exl-id: 978fe0d0-3917-4ba2-94bb-01c607a825cc
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# ACSD-52929: デフォルトのソース項目の再インデックスを実行する冗長リクエスト

ACSD-52929 パッチは、インベントリインデクサーが非同期モードで設定されている場合、デフォルトのソース項目を再インデックス化するリクエストの冗長性がある問題を修正しました。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.38 がインストールされている場合に使用できます。 パッチ ID は ACSD-52929 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6-p2

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

在庫インデクサーが非同期モードで設定されている場合、デフォルトのソース項目のインデックスを再作成するリクエストは冗長になります。

<u> 再現手順 </u>:

1. [!DNL RabbitMQ] の設定
1. **[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Catalog]**/**[!UICONTROL Inventory]**/**[!UICONTROL Inventory Indexer Setting]** に移動して、**[!UICONTROL Stock/Source reindex strategy]=[!UICONTROL Asynchronous]** を設定し、非同期のインデックス再作成戦略を有効にします。
1. カスタム在庫ソースを作成します。
1. [!DNL RabbitMQ] ダッシュボードにログインし、「キュー」タブに移動します。
1. キュー `inventory.indexer.sourceItem` チェックし、メッセージがないことを確認します。
1. バックエンドから単純な製品を開き、カスタムソースに *[!UICONTROL stock only]* を追加して、製品を保存します。
1. [!DNL RabbitMQ] ダッシュボードで `inventory.indexer.sourceItem` キューを読み込み、メッセージを確認します。

<u> 期待される結果 </u>:

カスタムソースのキューにはメッセージが 1 つしかありません。

<u> 実際の結果 </u>:

キューには 2 つのメッセージが表示されます。1 つはデフォルトソース用で、もう 1 つはカスタムソース用です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
