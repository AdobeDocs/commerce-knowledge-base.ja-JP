---
title: 設定が正しくないか、[!DNL OpCache]設定が欠落しているため、Cronが停止します
description: この記事では、設定が誤っているか、[!DNL OpCache]設定が欠落しているためにcronが機能しなくなる場合の解決策を提供します。
exl-id: 30643ea9-969f-41c8-8e62-b24e56d690cf
feature: Cache
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: b673188e-f9fa-492a-b470-c8f949bf7827
    internal-label: Cache
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%
---
# 設定が正しくないか、[!DNL OpCache]設定が欠落しているため、Cronが停止しました

この記事では、[!DNL OpCache]設定が欠落または誤って設定されたためにcronが機能しなくなる場合の解決策を提供します。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャ上のAdobe Commerce、[&#x200B; サポートされているすべてのバージョン &#x200B;](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)。

## イシュー

クローンが機能しなくなった。

## 原因

[!DNL OpCache] モジュールが新しいバージョンに更新され、ランタイムで`env.php`を書き換える[!DNL GraphQL] プラグインが導入され、cron設定が上書きされ、問題が発生した可能性があります。 `env.php file`の問題を回避するには、[!DNL OpCache]設定を更新する必要があります。これは、[!DNL ECE Tools] パッケージの[&#x200B; バージョン 2002.1.13](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/release-notes/ece-tools-package.html?lang=en#v2002.1.13)で解決されました。

## Solution

オプション 1: コマンドラインツールで次を実行します。

```bash
bin/magento cron:run
```

cronが無効になっていることを示すメッセージが表示されることがあります。

オプション 2: `app/etc/env.php` ファイルを開く – 以下が表示される場合は、cronが手動で無効になっているか、デプロイメントが失敗したため再度有効になっているか、問題は[!DNL OpCache]設定に関連していました。

```php
  'cron' =>
  array (
    'enabled' => 0,
  ),
```

1. cronが無効になっている場合は、このコマンドを実行してcronを再度有効にします：`vendor/bin/ece-tools cron:enable`
1. 最新バージョンの[!DNL ECE Tools]を使用していることを確認してください。 そうでない場合は、アップグレードしてください（または項目3にスキップしてください）。 既存のバージョンを確認するには、次のコマンドを実行します。
   `composer show magento/ece-tools`
1. 既に最新バージョンの[!DNL ECE Tools]を使用している場合は、`op-exclude.txt` ファイルが存在するかどうかを確認します。 これを行うには、次のコマンドを実行します。
   `ls op-exclude.txt`.
   このファイルが存在しない場合は、https://github.com/magento/magento-cloud/blob/master/op-exclude.txtをリポジトリに追加し、変更を確定して再デプロイします。
1. [!DNL ECE Tools]をアップグレードする必要はなく、リポジトリにhttps://github.com/magento/magento-cloud/blob/master/op-exclude.txtを追加または変更し、変更を確定して再デプロイすることもできます。

## 関連トピックス

* [Cronの準備状況チェックの問題](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues.html)
* [Crons プロパティ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/app/properties/crons-property.html)
* [Cron ジョブが「実行中」ステータスで停止している](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-job-is-stuck-in-running-status.html)
