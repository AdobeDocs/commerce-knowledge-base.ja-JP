---
title: Cron 準備チェックの問題
description: 「この記事では、cron 対応の問題に対する解決策を提供します。 cron の問題の症状を次に示します。」
exl-id: 1f2cee2c-98ad-4cf5-af16-d736fced2a15
feature: Configuration
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Cron 準備チェックの問題

この記事では、Cron 対応の問題に対する解決策を提供します。 cron の問題の症状を次に示します。

* PHP の設定 `$HTTP_RAW_POST_DATA` が正しく設定されていても、エラーメッセージが表示されます。
* 次の図に示すように、PHP レディネスチェックで PHP のバージョンが表示されません。
  ![upgr-tshoot-no-cron.png](assets/upgr-tshoot-no-cron.png)
* Commerce Admin に次のエラーが表示されます。
  ![compman-cron-not-running.png](assets/compman-cron-not-running.png)
このエラーを確認するには、次のように、ウィンドウの上部にある **システムメッセージ** をクリックする必要がある場合があります。
  ![compman_sys-messages.png](assets/compman_sys-messages.png)

## 既存の crontab の確認 {#check-your-existing-crontab}

この節では、cron が現在実行中かどうかを確認し、正しく設定されているかどうかを検証する方法について説明します。

crontab が設定されているかどうかを確認するには、次の手順に従います。

1. [MagentoのファイルシステムのオーナーとしてCommerce サーバーにログインするか、](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/file-system/overview) に切り替えます。
1. 次のファイルが存在するかどうかを確認します：`$ ls -al <magento_root>/var/.setup_cronjob_status`。 ファイルが存在する場合、cron は過去に正常に実行されています。 ファイル *が存在しない* 場合は、まだAdobe Commerceをインストールしていないか、cron が動作していません。 どちらの場合も、次の手順に進みます。
1. cron の詳細を見る。 `root` 権限を持つユーザーとして、次のコマンドを入力します：`$ crontab -u <Magento file system owner name> -l`。 例えば、CentOS `$ crontab -u magento_user -l` の場合は次のようになります。 ユーザーに crontab が設定されていない場合は、次のメッセージが表示されます。    `no crontab for magento_user`。 crontab には次の情報が表示されます。
   * 使用している PHP バイナリ （場合によっては複数のバイナリを使用）
   * 実行しているAdobe Commerce cron スクリプト（特に、それらのスクリプトへのパス）
   * Cron ログの場所

   問題の解決策については、次のいずれかの節を参照してください。

## 解決策：crontab が設定されていない {#solution-crontab-not-set-up}

Cron ジョブが正しく設定されていることを確認するには、開発者向けドキュメントの [cron ジョブの設定 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/next-steps/configuration) を参照してください。

## 解決策：間違った PHP バイナリから実行されている cron {#solution-cron-running-from-incorrect-php-binary}

Cron ジョブで web サーバープラグインとは異なる PHP バイナリを使用している場合は、PHP 設定エラーが表示される場合があります。 この問題を解決するには、PHP コマンドラインと PHP Web Server プラグインの両方に同じ PHP 設定を指定します。

PHP 設定について詳しくは、開発者向けドキュメントの [&#x200B; 必要な PHP 設定 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/php-settings) を参照してください。

## 解決策：cron がエラーで実行されている {#solution-cron-running-with-errors}

コマンドに役立つエラーメッセージが表示される可能性があるので、各コマンドを手動で実行してみてください。 開発者向けドキュメントの [cron ジョブの設定 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/next-steps/configuration) を参照してください。

>[!NOTE]
>
>ジョブを実行するには、cron を少なくとも *2 回* 実行する必要があります。最初にジョブをキューに入れ、2 回目にジョブを実行します。
