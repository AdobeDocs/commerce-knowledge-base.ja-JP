---
title: インストールに失敗しました。install.logを作成できません
description: この記事では、インストール中にセットアップウィザードで「install.log」が作成されないため、インストールに失敗した場合の修正について説明します。
exl-id: ff614018-8e49-4170-a806-8ebdc91ae8a9
feature: Install, Logs, Upgrade
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: a8ae7a5a-6cdc-5922-bd0d-6feb44b04984
    internal-label: Upgrade
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: 3c398179-d35a-51ba-b317-6c5b95feef5e
    internal-label: Logs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%
---
# インストールに失敗しました。install.logを作成できません

この記事では、セットアップ ウィザードがインストール中に`install.log`を作成しないため、インストールに失敗した場合の修正について説明します。

## イシュー

Adobe Commerce プロセスを同時に実行すると、インストールログの作成に問題が発生する可能性があります。 （例えば、別々のタブページにある2つの異なるインストール）。

## 原因

Installation-fails-cannot-create-install.log
`php.ini`の`open_basedir`の設定を確認してください。 セットアップ ウィザードでは、[sys\_get\_temp\_dir （void） ](https://php.net/manual/en/function.sys-get-temp-dir.php) PHP呼び出しを使用して、一時ディレクトリの値を取得します。 [open\_basedir](http://php.net/manual/en/ini.core.php#ini.open-basedir)が`sys_get_temp_dir`によって指定されたディレクトリへの接続を拒否するように設定されている場合、インストールは失敗します。
`php.ini`の`open_basedir`の設定を確認してください。 セットアップ ウィザードでは、[sys\_get\_temp\_dir （void） ](https://php.net/manual/en/function.sys-get-temp-dir.php) PHP呼び出しを使用して、一時ディレクトリの値を取得します。 [open\_basedir](https://php.net/manual/en/ini.core.php#ini.open-basedir)が`sys_get_temp_dir`によって指定されたディレクトリへの接続を拒否するように設定されている場合、インストールは失敗します。


## Solution

この問題を解決するには、値を`open_basedir`に変更し、Web サーバーを再起動します。

この値を変更する方法がわからない場合は、次の手順を使用します。

1. まだ行っていない場合は、[phpinfo.php](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/optional-software)を作成します。
1. ブラウザーのアドレスまたは場所フィールドに次のURLを入力してください：`https://<your web server IP or hostname>/<path to docroot>/phpinfo.php`
1. `php.ini`の場所を探します。`php.ini`は、通常、表示される結果で&#x200B;**読み込まれた設定ファイル**&#x200B;として指定されます。
1. ルート権限を持つユーザーは、テキストエディターで`php.ini`を開きます。
1. `open_basedir`の値を見つけて変更します。
1. 変更を`php.ini`に保存します。
1. Web サーバーを再起動します。
