---
title: インストールが失敗し、install.log を作成できない
description: この記事では、インストール中にセットアップ ウィザードが'install.log'を作成しなかったため、インストールに失敗した場合の解決策を示します。
exl-id: ff614018-8e49-4170-a806-8ebdc91ae8a9
feature: Install, Logs, Upgrade
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# インストールが失敗し、install.log を作成できない

この記事では、インストール中にセットアップ ウィザードが `install.log` を作成しなかったことが原因で発生したインストールの失敗を修正します。

## 問題

Adobe Commerce プロセスを同時に実行すると、インストールログの作成中に問題が発生する場合があります。 （例えば、別々のタブページに 2 つの異なるインストールがある場合）。

## 原因：

Installation-failes-cannot-create-install.log
`php.ini` で `open_basedir` の設定を確認します。 セットアップウィザードは、PHP 呼び出し [sys\_get\_temp\_dir （void）を使用して &#x200B;](https://php.net/manual/en/function.sys-get-temp-dir.php) 一時ディレクトリの値を取得します。 [open\_basedir](http://php.net/manual/en/ini.core.php#ini.open-basedir) が `sys_get_temp_dir` で指定されたディレクトリへの接続を拒否するように設定されている場合、インストールは失敗します。
`php.ini` で `open_basedir` の設定を確認します。 セットアップウィザードは、PHP 呼び出し [sys\_get\_temp\_dir （void）を使用して &#x200B;](https://php.net/manual/en/function.sys-get-temp-dir.php) 一時ディレクトリの値を取得します。 [open\_basedir](https://php.net/manual/en/ini.core.php#ini.open-basedir) が `sys_get_temp_dir` で指定されたディレクトリへの接続を拒否するように設定されている場合、インストールは失敗します。


## 解決策

この問題を解決するには、`open_basedir` の値を変更して、web サーバーを再起動します。

この値の変更方法が不明な場合は、次の手順を使用します。

1. まだ作成していない場合は、[phpinfo.php](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/optional-software) を作成します。
1. ブラウザーのアドレスまたは場所フィールドに、次の URL を入力します。`https://<your web server IP or hostname>/<path to docroot>/phpinfo.php`
1. `php.ini` の場所を探します。     通常、表示される結果では、`php.ini` は **読み込まれた設定ファイル** として指定されます。
1. root 権限を持つユーザーとして、`php.ini` をテキストエディターで開きます。
1. `open_basedir` の値を見つけて変更します。
1. `php.ini` に対する変更を保存します。
1. Web サーバーを再起動します。
