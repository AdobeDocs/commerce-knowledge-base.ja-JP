---
title: 'ACSD-49502：の後、ダウンロード可能なリンクが正しく更新されない [!DNL staging] 更新'
description: この後、ダウンロード可能なリンクが正しく更新されないAdobe Commerceの問題を修正するために、ACSD-49502 パッチを適用してください [!DNL staging] ダウンロード可能な製品にアップデートが適用されます。
exl-id: 9e7f0c06-4b7d-42c4-8ec7-cdeefd7e8a08
feature: Staging
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# ACSD-49502：の後、ダウンロード可能なリンクが正しく更新されない [!DNL staging] 更新

この ACSD-49502 パッチにより、ダウンロード可能なリンクが後に正しく更新されない問題が修正されます [!DNL staging] ダウンロード可能な製品にアップデートが適用されます。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.29 がインストールされています。 パッチ ID は ACSD-49502 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ダウンロード可能リンクが [!DNL staging] ダウンロード可能な製品にアップデートが適用されます。

<u>再現手順</u>:

1. リンクを含むダウンロード可能な製品を作成します。
1. 顧客アカウントを作成し、ログインします。
1. ダウンロード可能な製品をストアフロントからカートに追加します。
1. が含まれる **[!UICONTROL Admin]**、ダウンロード可能な製品の新しいアップデートをスケジュールし、スケジュールされたアップデートを完了させます。
1. ストアフロントで注文を完了します。

<u>期待される結果</u>:

ダウンロード可能なリンクは、以前に追加された製品が買い物かごに入っている間、スケジュールされた更新を使用する際に保持されます。

<u>実際の結果</u>:

ダウンロード可能なリンクが、お客様の *[!UICONTROL My Account]* （[!UICONTROL My Downloadable Products]）に設定し、でページの順序を指定します  **[!UICONTROL Admin]**.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
