---
title: 「[!UICONTROL Commerce Admin] ログインフォームに「現在のセッションの有効期限が切れました」というエラーが表示されてリダイレクトし直す」
description: 「この記事では、[!UICONTROL Commerce Admin] のログインの問題に対して考えられる解決策を提供します。この問題では、次のエラーメッセージでログインフォームにリダイレクトされます。*「現在のセッションの有効期限が切れました」*。 解決策には、サーバー時間設定の問題の確認や、セッションストレージ設定の変更が含まれます。'
exl-id: 29df2ed2-ff4a-4f1a-bdb7-1160416cda00
feature: Admin Workspace
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# 「現在のセッションの有効期限が切れました」というエラーが表示されて [!UICONTROL Commerce Admin] ログインフォームにリダイレクトし直します

この記事では、[!UICONTROL Commerce Admin] のログインの問題に対して考えられる解決策を示します。この問題では、次のエラーメッセージでログインフォームにリダイレクトされます。*「現在のセッションの有効期限が切れました」*。 解決策には、サーバー時間設定の問題の確認や、セッションストレージの設定の変更が含まれます。

## 影響を受けるエディションとバージョン：

すべてのAdobe Commerceのバージョンとエディション

## 問題

<u> 再現手順 </u>:

1. **[!UICONTROL Commerce Admin]** のページに移動します。
1. 資格情報を入力し、「**ログイン**」をクリックします。

<u> 期待される結果 </u>:

[!UICONTROL Commerce Admin] にログインします。

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

セッションストレージを変更してみてください。 開発者向けドキュメントの [ セッションファイルの探し方 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/storage/session-storage/sessions) 記事の情報を使用して、セッションが保存されている場所を確認し、`app/etc/env.php` ファイルを編集して変更します。

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

* 開発者向けドキュメントの [ 設定ファイルからデータを読み込む ](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/cli/configuration-management/import-configuration)
* 開発者向けドキュメントの [ 設定  [!DNL Redis]](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/cache/redis/config-redis)
* サポート技術情報で [ 「アカウントが一時的に無効になっています」というエラーが表示された [!UICONTROL Commerce Admin] ログインフォームにリダイレクト ](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/redirect-back-to-the-admin-login-form-with-your-account-is-temporarily-disabled-error) る
* [ サポートナレッジベースで [!UICONTROL Commerce Admin]](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/login-redirect-when-trying-to-login-to-magento-admin) にログインしようとすると、エラーが発生せずにログインフォームに戻ります
* Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/ja/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)

