---
title: 「アカウントが一時的に無効になっています」というエラーが表示されたCommerce管理者ログインフォームにリダイレクトし直します
description: 「この記事では、Commerce管理者のログイン問題に対して考えられる解決策を提供します。この問題では、次のエラーメッセージでログインフォームにリダイレクトされます。*「アカウントが一時的に無効になっています」*。 推奨される解決策は、管理者ユーザーデータベース設定を確認して修正することです。'
exl-id: 1c7ffa1c-1fb1-4f69-9534-77d1e119318a
feature: Admin Workspace, Customer Service
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 「アカウントが一時的に無効になっています」というエラーが表示されたCommerce管理者ログインフォームにリダイレクトし直します

この記事では、次のエラーメッセージでログインフォームにリダイレクトされるCommerce管理者のログインの問題に対して考えられる解決策を提供します。 *「アカウントが一時的に無効になっています」*. 推奨される解決策は、管理者ユーザーデータベースの設定を確認して修正することです。

## 影響を受けるエディションとバージョン：

すべてのAdobe Commerceのバージョンとエディション

## 問題

<u>再現手順</u>:

1. Commerceの「管理者」ページに移動します。
1. 資格情報を入力し、「ログイン」をクリックします。

<u>期待される結果</u>:

Commerce管理者にログインします。

<u>実際の結果</u>:

ログイン フォームにリダイレクトされ、次のエラーメッセージが表示されます。 *「アカウントが一時的に無効になります。 「後でもう一度試してください」*.

## 解決策

1. データベースバックアップを作成します。
1. 次のようなデータベースツールを使用します [phpMyAdmin](https://devdocs.magento.com/guides/v2.2/install-gde/prereq/optional.html#install-optional-phpmyadmin)または、コマンドラインから手動で DB にアクセスします。 が含まれる `admin_user` データベーステーブルの場合、管理者ユーザーレコードに対して、 `is_active` はに設定されています。`1```と `lock_expires` 等しい `NULL`. 必要に応じて、これらの値をリセットします。

## サポートナレッジベースの関連資料

* [Commerce管理者にログインしようとすると、エラーが発生せずにログインフォームに戻ります](/help/troubleshooting/miscellaneous/login-redirect-when-trying-to-login-to-magento-admin.md)
