---
title: 「ACSD-47054：すべてのストアのインデックスを再作成するとコンテンツのプレビューが遅くなる」
description: ACSD-47054 パッチを適用して、すべてのストアのインデックスを再作成したためにプレビューページの読み込みが遅くなるAdobe Commerceの問題を修正してください。
feature: Page Content
role: Admin, Developer
exl-id: 4dc61f78-7038-48ab-a2d3-9b05cf0c9b5c
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# ACSD-47054：すべてのストアのインデックスを再作成するとコンテンツのプレビューが遅くなる

ACSD-47054 パッチを使用すると、ストアが多数ある場合にコンテンツのステージングのプレビューの読み込みに時間がかかる問題を修正できます。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.37 がインストールされています。 パッチ ID は ACSD-47054 です。 この問題はAdobe Commerce 2.4.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法）:2.4.2-p2、2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法）:2.4.2 ～ 2.4.5-p4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

すべてのストアのインデックスが再作成されるので、プレビューページの読み込みに時間がかかる。

<u>再現手順</u>:

1. Commerce管理者に移動します。
1. スケジュールされている更新を作成します。
1. に移動 **[!UICONTROL Content]** > **[!UICONTROL Dashboard]**.
1. スケジュールされた更新をプレビューします。
1. 任意のカテゴリを開きます。

<u>期待される結果</u>:

プレビューページは、許容可能な時間内に読み込まれます。

<u>実際の結果</u>:

コンテンツのステージングのプレビューに時間がかかる。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
