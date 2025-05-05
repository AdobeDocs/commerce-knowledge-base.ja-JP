---
title: PHP バージョン準備チェックの問題
description: ここでは、Web Setup Wizard を使用してオンプレミスでAdobe Commerceをインストールまたはアップグレードする際に発生する可能性のある PHP バージョンの問題に対する解決策について説明します。
exl-id: dee939cf-b9b2-4750-965c-5b8908a4498d
feature: Variables
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# PHP バージョン準備チェックの問題

ここでは、Web Setup Wizard を使用してオンプレミスでAdobe Commerceをインストールまたはアップグレードする際に発生する可能性のある PHP バージョンの問題に対する解決策について説明します。

>[!WARNING]
>
>クラウドインフラストラクチャー上のAdobe Commerceでは、インフラストラクチャチームに 48 営業時間通知しない限り、サービスアップグレードを実稼動環境にプッシュすることはできません。 実稼動環境のダウンタイムを最小限に抑え、目的の期間内に設定を更新できるインフラストラクチャサポートエンジニアを確保する必要があるので、これが必要になります。 そのため、変更を実稼動環境で行う必要がある [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)48 時間前に、必要なサービスアップグレードの詳細と、アップグレードプロセスを開始する時刻を指定します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.2.x、2.3.x
* Magento Open Source2.2.x, 2.3.x

## サポートされていない PHP バージョン

### 問題

サポートされていない PHP バージョンを使用しているため、チェックは失敗します。

### 解決策

この問題を解決するには、開発者ドキュメント [2.3.x のシステム要件 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/system-requirements) および [2.2.x のシステム要件 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/system-requirements) にリストされているサポート対象バージョンのいずれかを使用します。

## PHP レディネスチェックが表示されない

### 問題

次の図に示すように、PHP レディネスチェックで PHP のバージョンが表示されません。
![upgr-tshoot-no-cron.png](assets/upgr-tshoot-no-cron.png)

### 解決策

これは、cron ジョブの設定が正しくない症状です。 詳しくは、開発者用ドキュメントの [cron ジョブの設定 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/next-steps/configuration) を参照してください。

## PHP バージョンが正しくありません

### 問題

このチェックは、不正な PHP バージョンを報告します。 通常、これは複数のバージョンの PHP をインストールしている上級ユーザにのみ発生します。 準備チェックが失敗する場合もあれば、合格する場合もあります。

レディネス・チェックで報告された PHP のバージョンが正しくない場合は、PHP CLI と Web サーバ・プラグインの間で PHP のバージョンが一致していないことが原因です。 Adobe Commerceでは、（cron を実行する） CLI と（Commerce管理、コンポーネントマネージャーおよびシステムアップグレードを実行する） web サーバーの両方で PHP の *1 つのバージョン* を使用する必要があります。

### 解決策

この問題がある場合は、システムに複数のバージョンの PHP をインストールしている可能性が高い上級ユーザーであると仮定します。

この問題を解決するには、次の操作を試してください。

* Web サーバーまたは php-fm を再起動します。
* `$PATH` 環境変数に PHP への複数のパスがあるかどうかをチェックします。
* `which php` コマンドを使用して、パス内の最初の PHP 実行可能ファイルを探します。正しくない場合は、そのファイルを削除するか、正しい PHP バージョンへのシンボリックリンクを作成します。
* [`phpinfo.php`](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/optional-software) ページを使用して、詳細情報を収集します。
* アドビの開発者向けドキュメントで、サポート対象の PHP バージョンを、アドビのシステム要件に従って実行していることを確認してください。
   * [Adobe Commerceの動作環境 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/system-requirements)
* 開発者向けドキュメントの [PHP 設定オプション ](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/system-requirements#php-settings) で説明されているように、PHP コマンドラインと PHP web サーバープラグインの両方に同じ PHP 設定を指定します。
