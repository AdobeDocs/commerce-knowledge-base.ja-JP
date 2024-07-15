---
title: 「MDVA-11189:CSV の読み込み後に cataloginventory_stock 行が削除される」
description: MDVA-11189 Adobe Commerce パッチでは、.csv ファイルを読み込んで商品ストックを更新した後、「cataloginventory_stock」テーブルの行が削除される問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.20 がインストールされている場合に利用できます。 パッチ ID は MDVA-1189。 この問題はAdobe Commerce 2.3.5 で修正されました。
exl-id: 84e1979c-826c-4c01-b0c7-8054bb4b23f0
feature: Catalog Management, Data Import/Export, Inventory, Orders
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# MDVA-11189: cataloginventory_stock 行が CSV のインポート後に削除されました

MDVA-11189 Adobe Commerce パッチでは、.csv ファイルを読み込んで商品ストックを更新した後、`cataloginventory_stock` テーブルの行が削除される問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.20 がインストールされている場合に使用できます。 パッチ ID は MDVA-1189。 この問題はAdobe Commerce 2.3.5 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** Cloud Infrastructure 2.2.3 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce（すべてのデプロイメント方法） 2.3.0-2.3.4-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

`.csv` を読み込んで製品ストックを更新した後に、`cataloginventory_stock` テーブルから行が削除される問題を修正しました。

<u> 再現手順：</u>

1. データベースで、次の MySQL コマンドを実行します。`select count(*) from cataloginventory_stock_status;`
1. 行数に注意してください。
1. crontab を次のように設定します。`* * * * * /usr/bin/php <path to installation>/bin/magento cron:run  | grep -v "Ran jobs by schedule" >> <path to installation>/var/log/cron.log 2>&1`
1. **システム**/**ツール**/**インデックス管理** の管理パネルに移動します。
1. インデクサーを *スケジュールに従って更新* に設定します
1. **システム**/*データ転送*/**エクスポート** に移動します。
1. **エンティティタイプ** を *製品*/**続行** に設定します。
1. 保存した `.csv` ファイルを開き、「SKU」と「QTY」を除くすべての列を削除します。
1. すべての製品の数量を 150 に更新します。
1. `.csv` ファイルを保存します。
1. **システム**/*データ転送*/**インポート** に移動します。
1. 次の値を設定します。
   1. エンティティタイプ：*Products*
   1. 読み込みの動作：*追加/更新*
   1. その他の値はデフォルトのままにします。
   1. 「ファイル」を選択して、カタログ製品スプレッドシートを選択します。
1. **データの確認**/**インポート** をクリックします。 5～10 分を通過させます。
1. データベースで、次の MySQL コマンドを実行します。
   `select count(*) from cataloginventory_stock_status;`

<u> 実際の結果：</u>

`cataloginventory_stock` の行数は、CSV の読み込み後に減らして在庫を更新します。

<u> 期待される結果：</u>

`cataloginventory_stock` の行数は、CSV の読み込み後も、同じままにして在庫を更新する必要があります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
