---
title: 「ACSD-52929：デフォルトのソース項目の再インデックスに対する冗長リクエスト」
description: インベントリインデクサーが非同期モードで設定されている場合、デフォルトのソース項目を再インデックスする冗長なリクエストが発生するAdobe Commerceの問題を修正するために、ACSD-52929 パッチを適用してください。
feature: Configuration, Inventory
role: Admin, Developer
exl-id: 978fe0d0-3917-4ba2-94bb-01c607a825cc
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# ACSD-52929: デフォルトのソース項目の再インデックスを実行する冗長リクエスト

ACSD-52929 パッチは、インベントリインデクサーが非同期モードで設定されている場合、デフォルトのソース項目を再インデックス化するリクエストの冗長性がある問題を修正しました。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.38 がインストールされています。 パッチ ID は ACSD-52929 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

在庫インデクサーが非同期モードで設定されている場合、デフォルトのソース項目のインデックスを再作成するリクエストは冗長になります。

<u>再現手順</u>:

1. 設定 [!DNL RabbitMQ].
1. に移動して、非同期のインデックス再作成戦略を有効にします。 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Inventory]** > **[!UICONTROL Inventory Indexer Setting]** およびを設定 **[!UICONTROL Stock/Source reindex strategy]=[!UICONTROL Asynchronous]**.
1. カスタム在庫ソースを作成します。
1. にログイン [!DNL RabbitMQ] ダッシュボードで、「キュー」タブに移動します。
1. チェック `inventory.indexer.sourceItem` キューに入れ、メッセージがないことを確認します。
1. バックエンドからシンプルな製品を開き、次を追加します *[!UICONTROL stock only]* をカスタムソースに追加して、製品を保存します。
1. を読み込みます `inventory.indexer.sourceItem` キュー内 [!DNL RabbitMQ] ダッシュボードでメッセージを確認します。

<u>期待される結果</u>:

カスタムソースのキューにはメッセージが 1 つしかありません。

<u>実際の結果</u>:

キューには 2 つのメッセージが表示されます。1 つはデフォルトソース用で、もう 1 つはカスタムソース用です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
