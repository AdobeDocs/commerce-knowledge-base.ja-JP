---
title: クラウドインフラストラクチャー上のAdobe Commerceで管理者パスワードを変更
description: '![login_panel_s.png] （assets/login_panel_s.png）'
exl-id: 1b6e867e-d314-4e7b-be95-d699e6749896
feature: Admin Workspace, Cloud
source-git-commit: 7dc84525aef4d59346bb9bc980a7ed9b7f6612cf
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# クラウドインフラストラクチャー上のAdobe Commerceで管理者パスワードを変更

## 方法 1：パスワードを忘れた場合（E メールによるリセット）

![login_panel_s.png](assets/login_panel_s.png)

ユーザーガイドの [ 管理者ログインのパスワードのリセット ](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/admin-signin.html#admin-sign-in) の手順をお読みください。

重要な使用上の注意を以下に示します。

### 送信メールを有効にする

**パスワードを忘れた場合** フォームを使用する前に、[&#128279;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html)Cloud Console[ を使用して ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/outgoing-emails.html) 送信メールを有効にする  を行います。

### 迷惑メール フォルダーの確認

パスワードのリセットリンクを含んだメッセージが見つからない場合は、「迷惑メール *フォルダーを確認し* ください。 メールの名前は *管理者ユーザー名のパスワードリセットの確認* です。

## 方法 2：新しい管理者ユーザーを追加する

既存のユーザーのパスワードを復元またはリセットできない場合は、新しい管理者ユーザーを作成して、このユーザーのパスワードを設定できます。 これを行うには、次の手順に従います。

1. [SSH を使用して、リモート環境にログインします ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html)。
1. 次のコマンドを実行します：`bin/magento admin:user:create   --admin-user=%user_name% --admin-password=%your_password% --admin-email=%your_email% --admin-firstname=%admin_user_first_name% --admin-lastname=%admin_user_last_name%`
