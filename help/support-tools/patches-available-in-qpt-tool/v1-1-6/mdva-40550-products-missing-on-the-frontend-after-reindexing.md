---
title: 「MDVA-40550：インデックス再作成後にフロントエンドに製品が表示されない」
description: MDVA-40550 パッチでは、インデックス再作成によって一部またはすべてのストアフロントカテゴリに製品が欠落する問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.6 がインストールされている場合に利用できます。 パッチ ID は MDVA-40550。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 0aca6eb2-6eb2-4ac4-8ae1-052f671c14e5
feature: Categories, Console, Products
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# MDVA-40550：インデックス再作成後にフロントエンドに製品が表示されない

MDVA-40550 パッチでは、インデックス再作成によって一部またはすべてのストアフロントカテゴリに製品が欠落する問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.6 がインストールされている場合に使用できます。 パッチ ID は MDVA-40550。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.5 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 再現手順 </u>:

1. 商品を作成します。
1. インデクサーを **スケジュールに従って更新** に切り替えます。
   * 製品をカテゴリに割り当てます。
1. `\Magento\Indexer\Model\Indexer::reindexAll` と `\Magento\Indexer\Model\IndexMutex::execute` で xdebug を有効にし、xdebug ブレークポイントを設定します。
1. `catalog_category_product` の **full reindex** をコマンドを使用して実行します。

   ```bash
   bin/magento indexer:reindex catalog_category_product
   ```

   * ブレークポイント `\Magento\Indexer\Model\Indexer::reindexAll` で実行が停止するまで待ちます。

1. 別のコンソールで、次のコマンドと並行して **部分的な再インデックス** を実行します。

   ```bash
   bin/magento cron:run --group=index --bootstrap=standaloneProcessStarted=1
   ```

1. ブレークポイント `\Magento\Indexer\Model\IndexMutex::execute` で実行が停止するまで待ちます。 `catalog_category_product` インデクサーがロックされます。
1. `catalog_category_product` の完全な再インデックスの実行を再開し、ロックタイムアウト（60 秒）待ちます。

<u> 期待される結果 </u>:

コンソールにエラーメッセージはありません。

<u> 実際の結果 </u>:

次のエラーが発生します。

*インデックス：catalog_category_product のロックを取得できませんでした*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
