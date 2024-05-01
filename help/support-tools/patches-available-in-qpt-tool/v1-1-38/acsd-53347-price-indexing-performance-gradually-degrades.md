---
title: 「ACSD-53347：価格インデックス作成のパフォーマンスが時間とともに徐々に低下」
description: ACSD-53347 パッチを適用すると、大規模な商品カタログのインデックスを再作成する際にパフォーマンスが徐々に低下するAdobe Commerceの問題を修正できます。
feature: Price Indexer
role: Admin
exl-id: 28795673-54b0-4282-bd43-344401cbe140
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# ACSD-53347：価格インデックス作成のパフォーマンスが時間とともに徐々に低下

ACSD-53347 パッチは、大規模な製品カタログの価格のインデックスを再作成するとパフォーマンスが徐々に低下する問題を修正しました。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.38 がインストールされています。 パッチ ID は ACSD-53347 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

大規模な製品カタログの価格のインデックスを再作成すると、インデックス作成プロセス中に実行されるクエリのパフォーマンスが徐々に低下します。

<u>再現手順</u>:

1. 大きなシンプルなカタログを作成し、これらの製品にカスタムオプションを割り当てます（カスタムオプションでは、インデックス作成時に一時テーブルを使用します）。
1. 少なくとも 200 以上の顧客グループを作成して、イシューの可視性を高めます。
1. 10 以上の web サイトを作成し、それぞれに製品をすべて割り当てます。
1. 読み込まれる製品はほぼ同じで、SKU と名前のみが異なります。
1. Enable （有効） **[!UICONTROL DB Logging]**.
1. を実行 `bin/magento index:reindex catalog_product_price` コマンド。
1. チェック対象 *DELETE元`catalog_product_index_price_opt_agr_temp`* が含まれる `db.log`.

<u>期待される結果</u>:

の実行 *DB クエリ* は効率的に実行されます。

<u>実際の結果</u>:

のパフォーマンス *DB クエリ* 一時テーブルの処理に時間がかかるため、価格インデックス作成テーブルの完了には多くの時間がかかります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
