---
title: 「ACSD-45071：読み込み時に製品に追加されたデフォルトソース」
description: ACSD-45071 パッチを使用すると、インポート時にデフォルトのソースが製品に追加される問題を解決できます。 このパッチは、[[!DNL Quality Patches Tool (QPT)]] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.21 がインストールされている。 パッチ ID は ACSD-45071 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: 8d8dbb06-6133-4d7a-939a-8bf18caec81c
feature: Data Import/Export, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# ACSD-45071：読み込み時に製品に追加されるデフォルトのソース

ACSD-45071 パッチを使用すると、インポート時にデフォルトのソースが製品に追加される問題を解決できます。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.21 がインストールされています。 パッチ ID は ACSD-45071 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.3-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品をインポートすると、デフォルトのソースが製品に自動的に割り当てられ、数量がゼロ、ステータスが在庫切れに設定されます。

<u>再現手順</u>:

1. 新規ソースを作成します。
1. 新しいソースを使用して新しい在庫を作成します。
1. Adobe Commerce管理の商品編集ページで、カスタム在庫のみを割り当て、ある程度の数量を設定し、在庫ステータスを「」に設定します。 **[!UICONTROL In Stock]**.
1. 次を介した製品の読み込み： **[!UICONTROL Admin]** > **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Import]**.

<u>期待される結果</u>:

デフォルトのソースは、インポート後に自動的には製品に割り当てられません。

<u>実際の結果</u>:

在庫切れステータスと数量ゼロでインポートすると、デフォルトソースが製品に割り当てられます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
