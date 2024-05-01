---
title: Cron のトラブルシューティング
description: この記事では、Adobe Commerce オンプレミス製品の cron に関する問題のトラブルシューティングソリューションについて説明します。
exl-id: e69a4fb3-731b-449e-a815-c33cd2faa567
feature: Configuration
role: Developer
source-git-commit: b6a79bcff3d757d40e7070182d8853a37960a782
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# Cron のトラブルシューティング

この記事では、Adobe Commerce オンプレミス製品の cron に関する問題のトラブルシューティングソリューションについて説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.2.x、2.3.x
* Magento Open Source2.2.x, 2.3.x

## 問題

## cron の問題の症状を次に示します。

* 更新またはアップグレードは実行されず、実行されません `pending` 都道府県。
* に関するエラーメッセージ [PHP](https://glossary.magento.com/php) 設定 `$HTTP_RAW_POST_DATA` が正しく設定されている場合でも表示されます。
* Cron の準備チェックが失敗します。 書き込み不可のパスや cron が設定されていない場合にエラーが発生します。 次に例を示します。

  ![upgr-tshoot-no-cron2.png](assets/upgr-tshoot-no-cron2.png)

* 次の図に示すように、PHP レディネスチェックで PHP のバージョンが表示されません。

  ![Screen_Shot_2019-08-29_at_1.36.08_PM.png](assets/Screen_Shot_2019-08-29_at_1.36.08_PM.png)

* Commerce Admin に次のエラーが表示されます。

  ![compman-cron-not-running.png](assets/compman-cron-not-running.png)

このエラーを確認するには、次をクリックする必要があります： **システムメッセージ** ウィンドウの上部に次のように表示されます。

![compman_sys-messages.png](assets/compman_sys-messages.png)

## 原因を調べる {#check-your-existing-crontab}

この節では、cron が現在実行中かどうかを調べ、適切に設定されているかどうかを確認する方法について説明します。

crontab が設定されているかどうかを確認するには、次の手順に従います。

1. Magentoサーバーに次のようにログインするか、 [Magento・ファイル・システムのオーナー](https://devdocs.magento.com/guides/v2.3/install-gde/prereq/file-sys-perms-over.html).
1. 次のファイルが存在するかどうかを確認します。    `bash    ls -al <magento_root>/var/.setup_cronjob_status`. ファイルが存在する場合、cron は過去に正常に実行されています。 ファイルが *次を含まない* Magentoをまだインストールしていないか、cron が動作していません。 どちらの場合も、次の手順に進みます。
1. cron の詳細を見る。 を使用した As a ユーザー `root` privileges。次のコマンドを入力します。    `bash    crontab -u <Magento file system owner name> -l`. 例：CentOS の場合 `bash    crontab -u magento_user -l`.  ユーザーに crontab が設定されていない場合は、次のメッセージが表示されます。    `terminal    no crontab for magento_user`. crontab には次の情報が表示されます。

   * 使用している PHP バイナリ （場合によっては複数のバイナリを使用）
   * 実行しているMagento cron スクリプト（特に、それらのスクリプトへのパス）
   * Cron ログの場所

問題の解決策については、次のいずれかの節を参照してください。

## 解決策

### crontab の解決策が設定されていない {#solution-crontab-not-set-up}

Cron ジョブが正しく設定されていることを確認するには、以下を参照してください。 [cron ジョブの設定](https://devdocs.magento.com/guides/v2.3/install-gde/install/post-install-config.html#post-install-cron).

### 間違った PHP バイナリから実行される cron の解決策 {#solution-cron-running-from-incorrect-php-binary}

Cron ジョブで web サーバープラグインとは異なる PHP バイナリを使用している場合は、PHP 設定エラーが表示される場合があります。 この問題を解決するには、PHP コマンドラインと PHP Web Server プラグインの両方に同じ PHP 設定を指定します。

PHP の設定の詳細については、を参照してください。 [必要な PHP 設定](https://devdocs.magento.com/guides/v2.3/install-gde/prereq/php-settings.html) 開発者向けドキュメントを参照してください。

### エラーが発生して実行されている cron のソリューション {#solution-cron-running-with-errors}

コマンドに役立つエラーメッセージが表示される可能性があるので、各コマンドを手動で実行してみてください。 参照： [cron ジョブの設定](https://devdocs.magento.com/guides/v2.3/install-gde/install/post-install-config.html#post-install-cron).

>[!NOTE]
>
>少なくとも cron を実行する必要があります *2 回* ジョブを実行する場合。ジョブを初めてキューに入れる場合は、ジョブを実行する 2 回目の場合です。
