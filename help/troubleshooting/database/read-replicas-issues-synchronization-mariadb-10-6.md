---
title: MariaDB 10.6 を使用したAdobe Commerce Cloud 2.4.6 のレプリカの問題を確認。
description: この記事では、MariaDB 10.6 でAdobe Commerce Cloud 2.4.6 のレプリカの読み取りに関する問題をトラブルシューティングする方法について説明します。
feature: Configuration
role: Developer,Admin
exl-id: b7af1cc3-93ff-40c5-8959-076cedddb56d
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
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

この `slave_parallel_mode` データベースの設定は、デフォルトでに変更されました。 *最適主義* 値をどのような場合に設定するか *保守的*、および `synchronous_replication` ece-Tools の値はデフォルトで *true* 値をどのような場合に設定するか *偽*.

## 解決策

1. を確認します。 `slave_parallel_mode` パラメーターはに設定されています。 *保守的* （次が必要です [サポートチケットを発行する](/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=en#submit-ticket) 値がとして表示されない場合 *保守的*）に設定します。 確認するには、次のコマンドを実行します。

   ```
    MariaDB [main]> show variables like 'slave_parallel_mode';
    +---------------------+--------------+
    | Variable_name       | Value        |
    +---------------------+--------------+
    | slave_parallel_mode | conservative |
    +---------------------+--------------+
    1 row in set (0.001 sec)
   ```

1. 更新 `.magento.env.yaml` データベース構成を次に示します。

   ```yaml
       DATABASE_CONFIGURATION:
        _merge: true
           slave_connection:
               default:
                   synchronous_replication: false
   ```



データベース設定の更新手順については、次を参照してください [DATABASE_CONFIGURATION](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html#database_configuration) クラウドインフラストラクチャガイドのCommerceにおける変数のデプロイのトピックを参照してください。


## 関連資料

* [デプロイメント用の環境変数の設定](/docs/commerce-cloud-service/user-guide/configure/env/configure-env-yaml.html) （Commerce on Cloud Infrastructure ガイド）を参照してください。
* [データベース設定のベストプラクティス](/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud.html) 実装プレイブック内。
