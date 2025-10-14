---
title: デプロイメントが失敗する Fastly モジュール互換性のないAdobe Commerce バージョン
description: '更新日：2019 年 2 月 29 日（PT）'
exl-id: aab77407-94e5-42de-92f4-2f0c19e24fa4
feature: Deploy, Extensions
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# デプロイメントが失敗する Fastly モジュール互換性のないAdobe Commerce バージョン

更新日：2019 年 2 月 29 日（PT）

ここでは、Fastly モジュールが現在のAdobe Commerceのバージョンと互換性がないことが原因でデプロイが失敗した場合の対応策を説明します。

**問題：** 新しいコミットおよびプッシュの後、デプロイメントが失敗し、次のようなエラーメッセージが表示されます。

>\[ 例外\] 警告：Fastly\\Cdn\\Plugin\\...の引数 3 が不足しています。これは/app/vendor/magento/framework/Interception/Interceptor.phpで呼び出され、/app/vendor/fastly/magento2/Plugin/ExcludeFilesFromMinification.phpで定義されています…

**原因：** Fastly モジュール v1.2.79 における後方互換性のない変更。

**解決策（一時的）:** Fastly モジュールをバージョン 1.2.82 以降にアップグレードし、新しい VCL をCommerce Admin にアップロードします。 その後、変更をコミットしプッシュして、デプロイメントが成功したことをトリガーします。

## 影響を受けるバージョン

* Adobe Commerce オンプレミス 2.1.X
* クラウドインフラストラクチャー 2.1.X 上のAdobe Commerce
* Fastly モジュール 1.2.79

## 問題

変更をコミットして統合、実稼働、またはステージング環境にプッシュする場合、通常、次の手順でデプロイメントプロセスをトリガーします。 これは、Adobe Commerce on cloud infrastructure edition では自動的に行われ、Adobe Commerceのオンプレミスでは手動で行われます。

デプロイメントが失敗し、次のエラーメッセージが表示される場合があります。

```
[2019-01-23 00:00:00] INFO: php ./bin/magento setup:static-content:deploy --ansi --no-interaction --jobs 1 --exclude-theme Magento/luma en_GB en_US
[2019-01-23 00:00:00] CRITICAL:
  Requested languages: en_GB, en_US
  Requested areas: frontend, adminhtml
  Requested themes: Magento/blank, Magento/backend
  === frontend -> Magento/blank -> en_GB ===

    [Exception]
    Warning: Missing argument 3 for Fastly\Cdn\Plugin\ExcludeFilesFromMinification::afterGetExcludes(), called in /app/vendor/magento/framework/Interception/Interceptor.php on line 152 and defined in /app/vendor/fastly/magento2/Plugin/ExcludeFilesFromMinification.php on line 38

  setup:static-content:deploy [-d|--dry-run] [--no-javascript] [--no-css] [--no-less] [--no-images] [--no-fonts] [--no-html] [--no-misc] [--no-html-minify] [-t|--theme[="..."]] [--exclude-theme[="..."]] [-l|--language[="..."]] [--exclude-language[="..."]] [-a|--area[="..."]] [--exclude-area[="..."]] [-j|--jobs[="..."]] [--symlink-locale] [languages1] ... [languagesN]

[2019-01-23 000:00:00] INFO: Set flag: var/.deploy_is_failed
[2019-01-23 00:00:00] CRITICAL: Command php ./bin/magento setup:static-content:deploy --ansi --no-interaction --jobs 1 --exclude-theme Magento/luma en_GB en_US returned code 1
```

クラウドインフラストラクチャソリューションでAdobe Commerceを使用している場合は、このエラーメッセージが [&#x200B; デプロイログ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/test/log-locations) に表示されます。 Adobe Commerce オンプレミスの場合は、コマンドラインにエラーが表示されます。

## 原因：

この問題は、Fastly モジュール v1.2.79 における後方互換性のない変更が原因です。

## 解決策

Fastly モジュールをバージョン 1.2.82 以降にアップグレードします。

これを行うには、次の手順を実行します。

1. 次のいずれかのコマンドを実行します。
   * fastly モジュールが magento-cloud-metapackage に含まれている場合：    <pre>composer update magento/magento-cloud-metapackage</pre>
   * fastly モジュールが個別にインストールされた場合（例えば、cloud edition ではなくAdobe Commerceをオンプレミスで使用している場合） <pre>composer update fastly/magento2</pre>
1. 変更内容をコミットしてプッシュし、デプロイメントプロセスをトリガーします（自動的に行われない場合）。
1. Admin で [&#x200B; 新しい VCL を Fastly にアップロードします &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration#upload-vcl-snippets)。
