---
title: 「ACSD-45071：読み込み時に製品に追加されたデフォルトソース」
description: ACSD-45071 パッチを使用すると、インポート時にデフォルトのソースが製品に追加される問題を解決できます。 このパッチは、[[!DNL Quality Patches Tool (QPT)]] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.21 がインストールされている場合に使用できます。 パッチ ID は ACSD-45071 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: 8d8dbb06-6133-4d7a-939a-8bf18caec81c
feature: Data Import/Export, Products
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# ACSD-45071：読み込み時に製品に追加されるデフォルトのソース

ACSD-45071 パッチを使用すると、インポート時にデフォルトのソースが製品に追加される問題を解決できます。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.21 がインストールされている場合に使用できます。 パッチ ID は ACSD-45071 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.3-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品をインポートすると、デフォルトのソースが製品に自動的に割り当てられ、数量がゼロ、ステータスが在庫切れに設定されます。

<u> 再現手順 </u>:

1. 新規ソースを作成します。
1. 新しいソースを使用して新しい在庫を作成します。
1. Adobe Commerce管理の商品編集ページで、カスタム在庫のみを割り当て、ある程度の数量を設定し、在庫ステータスを **[!UICONTROL In Stock]** に設定します。
1. **[!UICONTROL Admin]**/**[!UICONTROL System]**/**[!UICONTROL Data Transfer]**/**[!UICONTROL Import]** から製品を読み込みます。

<u> 期待される結果 </u>:

デフォルトのソースは、インポート後に自動的には製品に割り当てられません。

<u> 実際の結果 </u>:

在庫切れステータスと数量ゼロでインポートすると、デフォルトソースが製品に割り当てられます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
