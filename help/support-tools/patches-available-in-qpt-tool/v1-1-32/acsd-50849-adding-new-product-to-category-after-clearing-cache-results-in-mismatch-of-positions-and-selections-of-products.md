---
title: 「ACSD-50849：キャッシュをクリアした後に新しい製品を追加すると、不一致が発生する」
description: ACSD-50849 パッチを適用すると、キャッシュをクリアした後に新しい商品をカテゴリに追加すると、既存の商品の位置と選択内容が一致しなくなるAdobe Commerceの問題を修正できます。
feature: Cache, Categories, Products
role: Admin
exl-id: 3c797bf4-45da-4500-8c06-8c1007249738
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# ACSD-50849: キャッシュのクリア後に新しい製品を追加すると、不一致が発生する

ACSD-50849 パッチでは、キャッシュをクリアした後に新しい製品をカテゴリに追加すると、既存の製品の位置と選択内容が一致しなくなる問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) QPT 1.1.32 がインストールされました。 パッチ ID は ACSD-50849 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.5-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

キャッシュをクリアした後に新しい商品をカテゴリに追加すると、既存の商品の位置と選択内容が一致しなくなります。

<u>再現手順</u>:

1. 2 つの製品を作成します。
1. 1 つのカテゴリに 1 つの製品を割り当てます。
1. 管理者からカテゴリを開きます。
1. キャッシュのクリーンアップ `bin/magento cache:flush`.
1. 2 番目の製品をカテゴリに追加します。

<u>期待される結果</u>:

カテゴリに割り当てられた既存の製品は、自動的には削除されません。

<u>実際の結果</u>:

最初の（既存の）製品が自動的に削除されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
