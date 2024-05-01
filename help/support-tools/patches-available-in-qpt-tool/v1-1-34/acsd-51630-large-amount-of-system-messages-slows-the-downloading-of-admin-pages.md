---
title: 「ACSD-51630：多数のシステムメッセージが管理ページのダウンロードに時間がかかる」
description: ACSD-51630 パッチを適用すると、大量のシステムメッセージが表示されて管理ページのダウンロードが遅くなるAdobe Commerceのパフォーマンスの問題を修正できます。
feature: Admin Workspace, System
role: Admin
exl-id: 28f85199-625e-4299-bbca-8d2fc75df602
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# ACSD-51630：多数のシステムメッセージが表示され、管理ページのダウンロードが遅い

ACSD-51630 パッチは、大量のシステムメッセージが管理ページのダウンロードを遅らせるパフォーマンスの問題を修正します。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.34 がインストールされています。 パッチ ID は ACSD-51630 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 &lt; 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

多数のシステムメッセージが表示され、管理ページのダウンロードが遅い

<u>再現手順</u>:

1. DELETEへの多数のリクエストの実行（50,000 件を超える） `/rest/async/v1/products/ {sku}`.
1. アクセス （任意） **管理ページ**.

<u>期待される結果</u>:

適切な時間内にページが読み込まれます。 表示されているメッセージのみを読み込んでください。

<u>実際の結果</u>:

ページの読み込みに時間がかかりすぎます。 既存のメッセージはすべてデータベースから読み込まれます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
