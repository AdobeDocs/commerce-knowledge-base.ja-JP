---
title: 「アカウントが一時的に無効になっています」というエラーが発生して [!UICONTROL Commerce Admin] ログインフォームにリダイレクトし直す」
description: 「この記事では、Commerce管理者のログイン問題に対して考えられる解決策を提供します。この問題では、次のエラーメッセージでログインフォームにリダイレクトされます。*「アカウントが一時的に無効になっています」*。 推奨される解決策は、管理者ユーザーデータベース設定を確認して修正することです。'
exl-id: 1c7ffa1c-1fb1-4f69-9534-77d1e119318a
feature: Admin Workspace, Customer Service
role: Developer
source-git-commit: f87263cde5aa001f78abc368c949ce150feecb91
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---

# 「アカウントが一時的に無効になっています」というエラーが発生して [!UICONTROL Commerce Admin] ログインフォームにリダイレクトし直します

この記事では、[!UICONTROL Commerce Admin] のログインの問題に対して考えられる解決策を提供します。この問題が発生すると、次のエラーメッセージでログインフォームにリダイレクトされます。*「アカウントが一時的に無効になっています」*。 推奨される解決策は、管理者ユーザーデータベースの設定を確認して修正することです。

## 影響を受けるエディションとバージョン：

すべてのAdobe Commerceのバージョンとエディション

## 問題

<u> 再現手順 </u>:

1. **[!UICONTROL Commerce Admin]** のページに移動します。
1. 資格情報を入力し、「**ログイン**」をクリックします。

<u> 期待される結果 </u>:

[!UICONTROL Commerce Admin] にログインします。

<u> 実際の結果 </u>:

ログインフォームにリダイレクトされ、次のエラーメッセージが表示されます。*「アカウントが一時的に無効になっています。 後でもう一度お試しください」*。

## 解決策

1. データベースバックアップを作成します。
1. [[!DNL phpMyAdmin]](https://devdocs.magento.com/guides/v2.2/install-gde/prereq/optional.html#install-optional-phpmyadmin) などのデータベースツールを使用するか、コマンドラインから手動で DB にアクセスします。 `admin_user` データベース テーブルで、管理者ユーザーレコードに対して、`is_active` が&quot;`1`&quot;に設定され、`lock_expires` が `NULL` になっているかどうかを確認します。 必要に応じて、これらの値をリセットします。

## 関連資料

* [[!UICONTROL Commerce Admin]](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/login-redirect-when-trying-to-login-to-magento-admin) にログインしようとすると、エラーなしでログインフォームにリダイレクトし直す
* Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
