---
title: '「MDVA-32655: "quoteItemCleaner" コンシューマーが実行ごとに 1 つのメッセージを実行する」'
description: 複数の製品を削除した後、MDVA-32655 パッチにより、コンシューマー「quoteItemCleaner」の正しい「complete」メッセージに対する誤った「in progress」メッセージのステータスが修正されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.18 がインストールされている場合に利用できます。 パッチ ID は 32655 です。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。
exl-id: 07213430-f779-4a53-89fd-bc3905e13675
feature: Quotes
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# MDVA-32655: &quot;quoteItemCleaner&quot; コンシューマーは、実行ごとに 1 つのメッセージを実行します

MDVA-32655 パッチにより、誤った「進行中」メッセージ ステータスが、コンシューマー向けの正しい「完了」メッセージに修正されます `quoteItemCleaner` 複数の製品を削除した後。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.18 がインストールされています。 パッチ ID は 32655 です。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.3

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.0 - 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

この `quoteItemCleaner` コンシューマーは、各実行で 1 つのメッセージのみを実行します。

<u>再現手順</u>:

1. を確認します `queue_message_status` データベーステーブルを使用し、既存のすべてのキューメッセージが「完了」状態（ステータス ID 4）であることを確認します。
1. 自動Adobe Commerce cron 実行を停止します。
1. 2 つまたは 3 つの簡単な製品を作成します。
1. これら 3 つの簡単な製品を一括削除します。
1. が含まれる `queue_message_status` の新しいレコードが 3 つあることがわかります。 `catalog_product_removed_queue` トピック、状態 ID 2 （新しいレコード）。
1. 次のコマンドを実行して、これらを保留中に処理します `catalog_product_removed_queue` メッセージ：

   ```bash
   bin/magento queue:consumers:start quoteItemCleaner --single-thread --max-messages=100
   ```

<u>期待される結果</u>:

```sql
select * from queue_message_status s join queue q on s.queue_id = q.id where q.name = "catalog_product_removed_queue";
```

すべての `catalog_product_removed_queue` メッセージのステータスが「完了」（ID=4）に更新されます。

<u>実際の結果</u>:

3 つのうち 1 つのレコードのみが「完了」ステータスに更新されます（ID = 4）。 他の 2 つのメッセージのステータスは、ステータス ID = 3 （処理中）です。 未処理のキューメッセージを含んだバックログが生成される。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
