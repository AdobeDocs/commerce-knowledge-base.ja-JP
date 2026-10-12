---
title: MariaDB 10.6を使用したAdobe Commerce Cloud 2.4.6のレプリカに関する問題を読む
description: この記事では、Adobe Commerce Cloud 2.4.6とMariaDB 10.6のレプリカ読み取り問題のトラブルシューティング方法について説明します。
feature: Configuration
role: Developer,Admin
exl-id: b7af1cc3-93ff-40c5-8959-076cedddb56d
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%
---
# MariaDB 10.6を使用したAdobe Commerce Cloud 2.4.6のレプリカに関する問題を読む

この記事では、MariaDB 10.6以降でAdobe Commerce Cloud 2.4.6で読み取りレプリカを使用する際の予期しない動作に対する解決策を提供します。

## 影響を受ける製品とバージョン

* MariaDB 10.6以降
* Adobe Commerce on cloud infrastructure 2.4.6

## イシュー

非クリティカル読み取りで誤った情報が表示される。

## 原因

値を&#x200B;*保守的*&#x200B;にする必要がある場合、データベースの`slave_parallel_mode`設定はデフォルトで&#x200B;*楽観主義*&#x200B;に変更され、値を&#x200B;*false*&#x200B;にする必要がある場合、e-Toolsの`synchronous_replication`値はデフォルトで&#x200B;*true*&#x200B;になります。

## Solution

1. `slave_parallel_mode` パラメーターが&#x200B;*保守的*&#x200B;に設定されていることを確認します（値が&#x200B;*保守的*&#x200B;として表示されない場合は、[ サポートチケット ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=en#submit-ticket)を発行する必要があります）。 確認するには、次のコマンドを実行します。

   ```
    MariaDB [main]> show variables like 'slave_parallel_mode';
    +---------------------+--------------+
    | Variable_name       | Value        |
    +---------------------+--------------+
    | slave_parallel_mode | conservative |
    +---------------------+--------------+
    1 row in set (0.001 sec)
   ```

1. `.magento.env.yaml`個のデータベース設定を次の場所に更新します：

   ```yaml
       DATABASE_CONFIGURATION:
        _merge: true
           slave_connection:
               default:
                   synchronous_replication: false
   ```



データベース設定を更新する手順については、『Commerce on Cloud Infrastructure Guide 』の「Deploy variables」トピックの[DATABASE_CONFIGURATION](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html#database_configuration)を参照してください。


## 関連トピックス

* Commerce on Cloud Infrastructure ガイドの[ デプロイメント用の環境変数の設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/configure-env-yaml.html)。
* 実装プレイブックの[ データベース設定のベストプラクティス ](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud.html)。
