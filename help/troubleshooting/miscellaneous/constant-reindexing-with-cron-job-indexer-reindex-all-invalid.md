---
title: インデックスが無効化され、「indexer_reindex_all_invalid」が常に実行されます
description: インデックスが無効化され、「indexer_reindex_all_invalid」が常に実行されます
labels: troubleshooting,error,indexing,crons,site performance,adobe commerce,magento,cron,indexer_reindex_all_invalid,SQL,MySQL,reindex
exl-id: c7148ef4-2155-4d4c-869b-1d08de4af598
feature: B2B, Catalog Management, Categories, Observability, Price Indexer
role: Developer
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# インデックスは無効化され、継続的 `indexer_reindex_all_invalid` 実行されます

この記事では、継続的なインデックス再作成に起因するパフォーマンスの問題がサイトで発生した場合に、問題に対して考えられる回避策を提供します。 これは、[!DNL cron] ジョブが継続的に実行され、[!DNL reindex] でキャッシュ `indexer_reindex_all_invalid` クリーンアップされることが原因です。

## 影響を受ける製品とバージョン

* Adobe Commerce（クラウドおよびオンプレミス） 2.4.0 以降（**[!UICONTROL Category Permissions]** はAdobeCommerceのみの機能なので、Magento Open Sourceには影響しません）。

## 問題

[!DNL New Relic One] のエラーログには、1 秒を超える時間で何度も実行されている（つまり、何かを処理している） `indexer_update_all_views` が表示されます。

## 原因：

コア Adobe Commerce インポーターを（手動または [!DNL cron] で）実行すると、複数のコアモジュールをまたいだ一連のプラグインが実行され、無効化するインデックスが決定されます。

この問題は、[!DNL Commerce Admin] で **[!UICONTROL Category Permissions]** モジュールが有効になっている場合に発生します。 これが true の場合、モジュールのプラグインは、インポートの実行時に常に製品およびカテゴリインデックス（およびリンクインデックス）を無効にします。 標準の読み込みタイプを調べると、それらがすべて **[!UICONTROL Category Permissions]** に影響します。 無効化が必要です。

さらに、サイトで B2B モジュールが有効になっている場合、**[!UICONTROL Shared Catalog]** がアクティブになると、**[!UICONTROL Category Permissions]** のモジュールがオンになりロックされます。 **[!UICONTROL Shared Catalog]** をオフにするとロックは解除 **[!UICONTROL Category Permissions]** れますが、オフに切り替えることはできません。

<u>[!DNL MySQL] データベース内 [!DNL cron] ログを確認しています </u>:

[!DNL MySQL] データベースにログインすると、ロー **[!DNL reindex all indexes]** ルプロセスの `cron` ログを確認できます。
これは **必ず** 何度も表示されますが、重要な要因は、プロセスが 2 つの可能なことの 1 つを実行することです。

プロセスが実行できるのは、次の 2 つのうちいずれかのみです。

1. なし：0～1 秒（1 秒以下）かかります。プロセスは、何か実行する必要があるかどうかを確認し、何も実行する必要がない場合は停止します。
1. すべてを [!DNL Reindex] る：それは常に時間がかかります – 通常分。

通常、このプロセスの発生件数を多数確認したいのですが、実行時間は 1 秒未満です。
したがって、マーチャントはこの [!DNL MySQL] クエリを使用して、実行に **1 秒を超える** 時間がかかるトランザクションを検索できます。

```sql
SELECT TIMESTAMPDIFF(SECOND, executed_at, finished_at) AS period FROM cron_schedule WHERE job_code = 'indexer_reindex_all_invalid' HAVING period > 1
```

期間の記録期間は、次のコマンドを実行することで確認できます。

```sql
SELECT executed_at FROM cron_schedule WHERE job_code = 'indexer_reindex_all_invalid' AND executed_at IS NOT NULL ORDER BY executed_at ASC LIMIT 1;
```

適切に評価を行うのに十分な時間が得られない場合は、この [[!DNL Cron]  （スケジュールされたタスク）ガイドに従って成功した `cron` プロセスがログに保持される時間を増やし ](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cron.html?lang=ja)**[!DNL Success History Lifetime]** 値を増やすことができます（デフォルトは 60 分だけです）。


## 解決策

`afterImportSource` メソッドがカスタムインポーターを除外するように、`Magento\CatalogPermissions\Model\Indexer\Plugin\Import` を拡張します。

```
    public function afterImportSource(\Magento\ImportExport\Model\Import $subject, $import)
    {
        if ($this->config->isEnabled() && $subject->getEntity() !== 'ENTITY_CODE') {
            $this->indexerRegistry->get(\Magento\CatalogPermissions\Model\Indexer\Category::INDEXER_ID)->invalidate();
            $this->indexerRegistry->get(\Magento\CatalogPermissions\Model\Indexer\Product::INDEXER_ID)->invalidate();
        }
        return $import;
    }
```

ここで、`ENTITY_CODE` は、カスタムインポーターの `import.xml` ファイルのエンティティ名パラメーターに使用される値です。

## 関連資料

Adobe Commerce Operations Configuration Guide の [Configure [!DNL cron] jobs](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html?lang=ja)。
