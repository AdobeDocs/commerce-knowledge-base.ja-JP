---
title: インストールが失敗し、install.log を作成できない
description: この記事では、インストール中にセットアップ ウィザードが'install.log'を作成しなかったため、インストールに失敗した場合の解決策を示します。
exl-id: ff614018-8e49-4170-a806-8ebdc91ae8a9
feature: Install, Logs, Upgrade
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# インストールが失敗し、install.log を作成できない

この記事では、セットアップ ウィザードがインストールを作成しなかったために発生したインストールの問題を修正します。 `install.log` インストール中。

## 問題

Adobe Commerce プロセスを同時に実行すると、インストールログの作成中に問題が発生する場合があります。 （例えば、別々のタブページに 2 つの異なるインストールがある場合）。

## 原因：

Installation-failes-cannot-create-install.log 次の設定を確認します `open_basedir` 。対象： `php.ini`. セットアップ ウィザードでは、を使用します [sys\_get\_temp\_dir （void）](https://php.net/manual/en/function.sys-get-temp-dir.php) 一時ディレクトリの値を取得するための PHP のコール。 次の場合 [open\_basedir](http://php.net/manual/en/ini.core.php#ini.open-basedir) は、で指定されたディレクトリへの接続を拒否するように設定される `sys_get_temp_dir`の場合、インストールは失敗します。
の設定を確認してください `open_basedir` 。対象： `php.ini`. セットアップ ウィザードでは、を使用します [sys\_get\_temp\_dir （void）](https://php.net/manual/en/function.sys-get-temp-dir.php) 一時ディレクトリの値を取得するための PHP のコール。 次の場合 [open\_basedir](https://php.net/manual/en/ini.core.php#ini.open-basedir) は、で指定されたディレクトリへの接続を拒否するように設定される `sys_get_temp_dir`の場合、インストールは失敗します。


## 解決策

この問題を解決するには、の値を変更します `open_basedir` web サーバーを再起動します。

この値の変更方法が不明な場合は、次の手順を使用します。

1. まだの場合は、次を作成します [phpinfo.php](https://devdocs.magento.com/guides/v2.3/install-gde/prereq/optional.html#install-optional-phpinfo).
1. ブラウザーのアドレスまたは場所フィールドに、次の URL を入力します。 `https://<your web server IP or hostname>/<path to docroot>/phpinfo.php`
1. 場所を探す `php.ini`.     `php.ini` は通常、として指定されます **設定ファイルを読み込みました** 表示された結果で。
1. root 権限を持つユーザーとして、を開きます。 `php.ini` テキストエディター。
1. の値を見つけます。 `open_basedir` そして、それを変更します。
1. 変更をに保存します。 `php.ini`.
1. Web サーバーを再起動します。
