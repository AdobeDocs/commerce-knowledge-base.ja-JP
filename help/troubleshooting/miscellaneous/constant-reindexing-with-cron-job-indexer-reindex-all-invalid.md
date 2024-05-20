---
title: インデックスが無効化され、「indexer_reindex_all_invalid」が常に実行されます
description: インデックスが無効化され、「indexer_reindex_all_invalid」が常に実行されます
labels: troubleshooting,error,indexing,crons,site performance,adobe commerce,magento,cron,indexer_reindex_all_invalid,SQL,MySQL,reindex
exl-id: c7148ef4-2155-4d4c-869b-1d08de4af598
feature: B2B, Catalog Management, Categories, Observability, Price Indexer
role: Developer
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# インデックスが無効化されました。 `indexer_reindex_all_invalid` 絶えず走る

この記事では、継続的なインデックス再作成に起因するパフォーマンスの問題がサイトで発生した場合に、問題に対して考えられる回避策を提供します。 この問題は、 [!DNL cron] ジョブ `indexer_reindex_all_invalid` 継続的に実行され、でクリーンアップされたキャッシュ [!DNL reindex].

## 影響を受ける製品とバージョン

* Adobe Commerce（クラウドおよびオンプレミス） 2.4.0 以降（As） **[!UICONTROL Category Permissions]** はAdobeCommerceのみの機能であり、Magento Open Sourceには影響しません）。

## 問題

対象： [!DNL New Relic One] エラーログに次を表示 `indexer_update_all_views` 1 秒を超える時間（つまり、何かを処理している）で複数回実行している。

## 原因：

コア Adobe Commerce インポーターが（手動または [!DNL cron]その後、複数のコアモジュールにまたがる一連のプラグインが実行され、無効化するインデックスが決定されます。

この問題は、 **[!UICONTROL Category Permissions]** モジュールは [!DNL Commerce Admin]. これが true の場合、モジュールのプラグインは、インポートの実行時に常に製品およびカテゴリインデックス（およびリンクインデックス）を無効にします。 標準の読み込みタイプを調べると、それらがすべて影響します **[!UICONTROL Category Permissions]**. 無効化が必要です。

さらに、サイトで B2B モジュールが有効になっている場合、 **[!UICONTROL Shared Catalog]** アクティブ化され、オンおよびロックされます **[!UICONTROL Category Permissions]**. オフにする **[!UICONTROL Shared Catalog]** ロックを解除します **[!UICONTROL Category Permissions]**&#x200B;ただし、オフにしないでください。

<u>確認中 [!DNL cron] のログイン [!DNL MySQL] データベース</u>:

にログインする場合 [!DNL MySQL] データベースがある場合は、 `cron` のログ **[!DNL reindex all indexes]** プロセス。
この **すべき** 何度も現れますが、重要な要因は、プロセスが 2 つの可能なことの 1 つをすることです。

プロセスが実行できるのは、次の 2 つのうちいずれかのみです。

1. なし：0～1 秒（1 秒以下）かかります。プロセスは、何か実行する必要があるかどうかを確認し、何も実行する必要がない場合は停止します。
1. [!DNL Reindex] すべて：それは常に時間がかかります – 通常分。

通常、このプロセスの発生件数を多数確認したいのですが、実行時間は 1 秒未満です。
したがって、マーチャントはこれを使用できます [!DNL MySQL] 実行するトランザクションを検索するクエリ **more than 1 second** 実行する手順：

```sql
SELECT TIMESTAMPDIFF(SECOND, executed_at, finished_at) AS period FROM cron_schedule WHERE job_code = 'indexer_reindex_all_invalid' HAVING period > 1
```

期間の記録期間は、次のコマンドを実行することで確認できます。

```sql
SELECT executed_at FROM cron_schedule WHERE job_code = 'indexer_reindex_all_invalid' AND executed_at IS NOT NULL ORDER BY executed_at ASC LIMIT 1;
```

適切な評価を行うのに十分な期間が得られない場合は、成功するまでの時間を長くすることができます `cron` プロセスはこの後もログに保持されます [[!DNL Cron] （スケジュールされたタスク）](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cron.html) をガイドして増やす **[!DNL Success History Lifetime]** 値（デフォルトは 60 分のみ）。


## 解決策

Extend `Magento\CatalogPermissions\Model\Indexer\Plugin\Import` その結果、 `afterImportSource` メソッドを指定すると、カスタムインポーターが除外されます。

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

ここで、 `ENTITY_CODE` は、のエンティティ名パラメーターに使用される値です `import.xml` カスタムインポーターのファイル。

## 関連資料

[設定 [!DNL cron] ジョブ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html) （Adobe Commerce運用設定ガイド）を参照してください。
