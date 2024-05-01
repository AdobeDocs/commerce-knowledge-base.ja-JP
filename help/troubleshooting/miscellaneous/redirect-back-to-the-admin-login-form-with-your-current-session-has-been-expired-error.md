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

この記事では、次のエラーメッセージでログインフォームにリダイレクトされるCommerce管理者のログインの問題に対する解決策を説明します。 *「現在のセッションの有効期限が切れています」*. 解決策には、サーバー時間設定の問題の確認や、セッションストレージの設定の変更が含まれます。

## 影響を受けるエディションとバージョン：

すべてのAdobe Commerceのバージョンとエディション

## 問題

<u>再現手順</u>:

1. Commerceの「管理者」ページに移動します。
1. 資格情報を入力し、「ログイン」をクリックします。

<u>期待される結果</u>:

Commerce管理者にログインします。

<u>実際の結果</u>:

ログイン フォームにリダイレクトされ、次のエラーメッセージが表示されます。 *「現在のセッションの有効期限が切れています」*.

## 原因：

この問題には、次の 2 つの理由が考えられます。

* サーバー時間設定の問題
* セッションストレージの問題

解決策については、次の節を確認してください。

## 解決策

### サーバー時間設定の問題を確認します

で作成したセッションレコードを確認します。 `admin_user_session` テーブル。 次の値 `created_at` および/または `updated_at` が正しくありません。サーバー時間設定の問題が原因である可能性があります。 確認するには、サーバーのシステム管理者に問い合わせてください。 なお、DB の時間は、デフォルトで UTC に設定されています。

### セッションストレージの変更

セッションストレージを変更してみてください。 の情報を使用します [セッションファイルの見つけ方](https://devdocs.magento.com/guides/v2.3/config-guide/sessions.html) セッションの保存場所を確認し、を編集して変更するための開発者向けドキュメントの記事 `app/etc/env.php` ファイル。

例えば、ファイルシステムへのセッションの保存を開始するには、以下を変更します。 `'session'` セクションを次のように設定します。

```php
....
'session' =>
    array (
      'save' => 'files',
),
....
```

を実行 `bin/magento app:config:import` 設定データを読み込むコマンド。


## 関連資料

* [設定ファイルからのデータの読み込み](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-config-mgmt-import.html) 開発者向けドキュメントで
* [Redis の設定](https://devdocs.magento.com/guides/v2.3/config-guide/redis/config-redis.html) 開発者向けドキュメントで
* [「アカウントが一時的に無効になっています」というエラーが表示されたCommerce管理者ログインフォームにリダイレクトし直します](/help/troubleshooting/miscellaneous/redirect-back-to-the-admin-login-form-with-your-account-is-temporarily-disabled-error.md) サポートナレッジベースで
* [Commerce管理者にログインしようとすると、エラーが発生せずにログインフォームに戻ります](/help/troubleshooting/miscellaneous/login-redirect-when-trying-to-login-to-magento-admin.md) サポートナレッジベースで
