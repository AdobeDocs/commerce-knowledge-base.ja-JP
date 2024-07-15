---
title: MariaDB 10.6 を使用したAdobe Commerce Cloud 2.4.6 のレプリカの問題を確認。
description: この記事では、MariaDB 10.6 でAdobe Commerce Cloud 2.4.6 のレプリカの読み取りに関する問題をトラブルシューティングする方法について説明します。
feature: Configuration
role: Developer,Admin
exl-id: b7af1cc3-93ff-40c5-8959-076cedddb56d
source-git-commit: f12e25ac5dd607cc614dd99c90c5e104b2cee6a8
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# MariaDB 10.6 を使用したAdobe Commerce Cloud 2.4.6 のレプリカの問題を確認。

この記事では、Adobe Commerce Cloud 2.4.6 で MariaDB 10.6 以降にレプリカの読み取りを使用する際に発生した予期しない動作に対するソリューションを提供します。

## 影響を受ける製品とバージョン

* MariaDB 10.6 以降
* クラウドインフラストラクチャー上のAdobe Commerce 2.4.6

## 問題

重要でない読み取りで、誤った情報が表示される。

## 原因：

値を *保守的* にする必要がある場合、データベースの `slave_parallel_mode` 設定はデフォルトで *optimistics* に変更され、Ece-Tools の `synchronous_replication` 値は、値を *false* にする場合に *true* にデフォルト設定されています。

## 解決策

1. `slave_parallel_mode` パラメーターが *conservative* に設定されていることを確認します（値が *conservative* と表示されていない場合は、[ サポートチケットを発行 ](/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=en#submit-ticket) する必要があります）。 確認するには、次のコマンドを実行します。

   ```
    MariaDB [main]> show variables like 'slave_parallel_mode';
    +---------------------+--------------+
    | Variable_name       | Value        |
    +---------------------+--------------+
    | slave_parallel_mode | conservative |
    +---------------------+--------------+
    1 row in set (0.001 sec)
   ```

1. `.magento.env.yaml` データベース設定を次のように更新します。

   ```yaml
       DATABASE_CONFIGURATION:
        _merge: true
           slave_connection:
               default:
                   synchronous_replication: false
   ```



データベース設定を更新する手順については、Cloud Infrastructure ガイドのCommerceにある「変数のデプロイ」トピックの [DATABASE_CONFIGURATION](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html#database_configuration) を参照してください。


## 関連資料

* Commerce on Cloud Infrastructure ガイドの [ デプロイメント用の環境変数の設定 ](/docs/commerce-cloud-service/user-guide/configure/env/configure-env-yaml.html)。
* 実装プレイブックの [ データベース設定のベストプラクティス ](/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud.html)。
