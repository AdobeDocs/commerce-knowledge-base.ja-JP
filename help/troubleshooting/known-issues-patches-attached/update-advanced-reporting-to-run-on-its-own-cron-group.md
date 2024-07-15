---
title: 独自の cron グループで実行するように詳細レポートを更新
description: この記事では、Cloud Infrastructure 2.3.0 上のAdobe Commerceで高度なレポートにデータが表示されない既知の問題のパッチを提供します。 これは、高度なレポートジョブ「analytics_collect_data」がスケジュールに従って実行されないためです。 この記事では、詳細レポートの cron グループ「analytics」を作成するパッチを提供します。
exl-id: 8aff9e2b-d9be-4136-975b-05963e23f55c
feature: Configuration
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# 独自の cron グループで実行するように詳細レポートを更新

この記事では、Cloud Infrastructure 2.3.0 上のAdobe Commerceで高度なレポートにデータが表示されない既知の問題のパッチを提供します。 これは、高度なレポートジョブ `analytics_collect_data` がスケジュールに従って実行されないからです。 この記事では、詳細レポートの cron グループ `analytics` を作成するパッチを提供します。

## 問題

詳細レポートモジュールに読み込まれるデータはありません。

## パッチ

パッチはこの記事に添付されています。 このパッチは、`analytics` cron ジョブタスクをデフォルトグループから `analytics` に移動します。

ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[MDVA-19640\_EE\_2.3.0\_COMPOSER\_v1.patch](assets/MDVA-19640_EE_2.3.0_COMPOSER_v1.patch.zip)

パッチを適用した後、次の SQL クエリを実行します。 テーブル内のレコードを変更するには、クエリを実行する必要 `cron_schedule` あります。

```
UPDATE core_config_data
SET `path` = REPLACE(path, "crontab/default/jobs/analytics", "crontab/analytics/jobs/analytics")
WHERE `path` LIKE "crontab/default/jobs/analytics%";
```

### 互換性のあるAdobe Commerceのバージョン：

パッチが作成された対象

* クラウドインフラストラクチャー 2.3.0 上のAdobe Commerce

このパッチは、Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure のAdobe Commerce バージョンとエディション 2.2.2-2.2.10、2.3.0-2.3.2 および 2.3.2-p2 と 2.3.3 でも互換性があります（ただし、問題が解決する可能性があります）

## パッチの適用方法

手順については、[Adobeが提供する Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。

## 添付ファイル
