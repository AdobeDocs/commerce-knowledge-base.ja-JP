---
title: Fastly module incompatible Adobe Commerce versionのデプロイメントに失敗する
description: 更新日：2019年2月29日（PT）
exl-id: aab77407-94e5-42de-92f4-2f0c19e24fa4
feature: Deploy, Extensions
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# Fastly module incompatible Adobe Commerce versionのデプロイメントに失敗する

更新日：2019年2月29日（PT）

この記事では、Fastly モジュールが現在のAdobe Commerce バージョンと互換性がないためにデプロイメントが失敗した場合の修正について説明します。

**問題：** デプロイメントは、新しいコミットとプッシュの後に失敗し、次のようなエラーメッセージが表示されます。

>\[Exception\]警告：Fastly\\Cdn\\Plugin\\...の引数3がありません。/app/vendor/magento/framework/Interception/Interceptor.php ...で呼び出され、/app/vendor/fastly/magento2/Plugin/ExcludeFilesFromMinification.php ...で定義されています。

Fastly モジュール v1.2.79の&#x200B;**原因：**&#x200B;後方互換性のない変更。

**解決策（一時的）:** Fastly モジュールをバージョン 1.2.82以降にアップグレードし、新しいVCLをCommerce Adminにアップロードします。 次に、変更を確定してプッシュし、デプロイメントを成功に導くトリガーを得ます。

## 影響のあるバージョン

* Adobe Commerce オンプレミス 2.1.X
* Adobe Commerce on cloud infrastructure 2.1.X
* Fastly モジュール 1.2.79

## イシュー

変更をコミットして統合、実稼動環境またはステージング環境にプッシュすると、通常、次の手順はデプロイメントプロセスのトリガーになります。 これは、Adobe Commerce on cloud infrastructure editionで自動的に行われ、Adobe Commerce オンプレミスで手動で行われます。

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

Adobe Commerce on cloud infrastructure ソリューションを使用している場合、[&#x200B; デプロイログ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/test/log-locations)にこのエラーメッセージが表示されます。 Adobe Commerce オンプレミスの場合、コマンドラインにエラーが表示されます。

## 原因

この問題は、Fastly モジュール v1.2.79の後方互換性のない変更が原因で発生します。

## Solution

Fastly モジュールをバージョン 1.2.82以降にアップグレードします。

これを行うには、次の手順を実行します。

1. 次のいずれかのコマンドを実行します。
   * magento-cloud-metapackageにFastly モジュールが含まれている場合：    <pre>composer update magento/magento-cloud-metapackage</pre>
   * fastly モジュールが個別にインストールされている場合（例えば、cloud editionではなくAdobe Commerce オンプレミスを使用している場合） <pre>composer update fastly/magento2</pre>
1. 変更を確定してプッシュし、デプロイメントプロセスが自動的に実行されない場合はトリガーします。
1. 管理画面で、[新しいVCLをFastly](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration#upload-vcl-snippets)にアップロードします。
