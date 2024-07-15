---
title: 「現在のセッションの有効期限が切れました」というエラーが表示されたCommerce管理者ログインフォームにリダイレクトし直します
description: 「この記事では、Commerce管理者のログインの問題に対して考えられる解決策を提供します。この問題では、次のエラーメッセージでログインフォームにリダイレクトされます。*「現在のセッションの有効期限が切れました」*。 解決策には、サーバー時間設定の問題の確認や、セッションストレージ設定の変更が含まれます。'
exl-id: 29df2ed2-ff4a-4f1a-bdb7-1160416cda00
feature: Admin Workspace
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 「現在のセッションの有効期限が切れました」というエラーが表示されたCommerce管理者ログインフォームにリダイレクトし直します

この記事では、Commerce管理者のログインの問題に対して考えられる解決策を示します。この問題では、次のエラーメッセージが表示されてログインフォームにリダイレクトされます。*「Your current session has been expired」*。 解決策には、サーバー時間設定の問題の確認や、セッションストレージの設定の変更が含まれます。

## 影響を受けるエディションとバージョン：

すべてのAdobe Commerceのバージョンとエディション

## 問題

<u> 再現手順 </u>:

1. Commerceの「管理者」ページに移動します。
1. 資格情報を入力し、「ログイン」をクリックします。

<u> 期待される結果 </u>:

Commerce管理者にログインします。

<u> 実際の結果 </u>:

ログインフォームにリダイレクトされ、次のエラーメッセージが表示されます。*「現在のセッションの有効期限が切れました」*。

## 原因：

この問題には、次の 2 つの理由が考えられます。

* サーバー時間設定の問題
* セッションストレージの問題

解決策については、次の節を確認してください。

## 解決策

### サーバー時間設定の問題を確認します

`admin_user_session` テーブルで作成されたセッションレコードを確認します。 `created_at` や `updated_at` の値が正しくない場合は、サーバー時間設定の問題が原因である可能性があります。 確認するには、サーバーのシステム管理者に問い合わせてください。 なお、DB の時間は、デフォルトで UTC に設定されています。

### セッションストレージの変更

セッションストレージを変更してみてください。 開発者向けドキュメントの [ セッションファイルの探し方 ](https://devdocs.magento.com/guides/v2.3/config-guide/sessions.html) 記事の情報を使用して、セッションが保存されている場所を確認し、`app/etc/env.php` ファイルを編集して変更します。

例えば、ファイルシステムへのセッションの保存を開始するには、`'session'` セクションを次のように変更します。

```php
....
'session' =>
    array (
      'save' => 'files',
),
....
```

`bin/magento app:config:import` コマンドを実行して、設定データを読み込みます。


## 関連資料

* 開発者向けドキュメントの [ 設定ファイルからデータを読み込む ](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-config-mgmt-import.html)
* アドビの開発者向けドキュメントの [Redis の設定 ](https://devdocs.magento.com/guides/v2.3/config-guide/redis/config-redis.html)
* サポートナレッジベースで [ 「アカウントが一時的に無効になっています」というエラーが表示されて ](/help/troubleshooting/miscellaneous/redirect-back-to-the-admin-login-form-with-your-account-is-temporarily-disabled-error.md)Commerce管理者ログインフォームにリダイレクトし直します
* [Commerce管理者にログインしようとすると、エラーが発生せずにログインフォームにリダイレクトし直します ](/help/troubleshooting/miscellaneous/login-redirect-when-trying-to-login-to-magento-admin.md)。サポートナレッジベースを参照
