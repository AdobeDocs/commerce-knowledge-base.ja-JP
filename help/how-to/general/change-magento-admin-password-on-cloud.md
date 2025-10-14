---
title: クラウドインフラストラクチャー上のAdobe Commerceで管理者パスワードを変更
description: '![login_panel_s.png] （assets/login_panel_s.png）'
exl-id: 1b6e867e-d314-4e7b-be95-d699e6749896
feature: Admin Workspace, Cloud
source-git-commit: 44238f6d57458028cb1e2612d45e1e12b3f39916
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# クラウドインフラストラクチャー上のAdobe Commerceで管理者パスワードを変更

## 方法 1：パスワードを忘れた場合（E メールによるリセット）

![login_panel_s.png](assets/login_panel_s.png)

ユーザーガイドの [&#x200B; 管理者ログインのパスワードのリセット &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/admin-signin.html?lang=ja#admin-sign-in) の手順をお読みください。

重要な使用上の注意を以下に示します。

### 送信メールを有効にする

**パスワードを忘れた場合** フォームを使用する前に、[&#128279;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html?lang=ja)Cloud Console[&#x200B; を使用して &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/outgoing-emails.html?lang=ja) 送信メールを有効にする  ことを確認してください。 これは、統合環境とサンドボックスプロジェクトにのみ適用されます。

実稼動環境またはステージング環境で送信メールが本当に無効になっている（つまり、メールが SendGrid で取得されなかった）場合は、「[Cloud Console でメールを有効にする &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/project/outgoing-emails#enable-emails-in-the-cli)」をオンにすることで、これを確認できます。 問題が解決しない場合は、Adobe[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) を送信できます。

### 迷惑メール フォルダーの確認

パスワードのリセットリンクを含んだメッセージが見つからない場合は、「迷惑メール *フォルダーを確認し* ください。 メールの名前は *管理者ユーザー名のパスワードリセットの確認* です。

## 方法 2：新しい管理者ユーザーを追加する

既存のユーザーのパスワードを復元またはリセットできない場合は、新しい管理者ユーザーを作成して、このユーザーのパスワードを設定できます。 これを行うには、次の手順に従います。

1. [SSH を使用して、リモート環境にログインします &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html?lang=ja)。
1. 次のコマンドを実行します：`bin/magento admin:user:create   --admin-user=%user_name% --admin-password=%your_password% --admin-email=%your_email% --admin-firstname=%admin_user_first_name% --admin-lastname=%admin_user_last_name%`
