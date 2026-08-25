---
title: Commerce Adminへのログイン時にリダイレクトする
description: この記事では、管理者にログインしようとするとログインフォームにリダイレクトされ、エラーメッセージが表示されない、Commerce管理者のログインに関する問題の解決策を説明します。 これには、Adobe Commerceのサーバータイムゾーン設定の修正とCookie設定のクリアが含まれます。
exl-id: ff3114fd-8690-4983-8221-cf807f083b15
feature: Admin Workspace, Cache
role: Developer
source-git-commit: ec2111316458420c51a6b6f3b3881bd3f9d10c06
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Commerce Adminへのログイン時にリダイレクトする

この記事では、管理者にログインしようとするとログインフォームにリダイレクトされ、エラーメッセージが表示されない、Commerce管理者のログインに関する問題の解決策を説明します。 これには、Adobe Commerceのサーバータイムゾーン設定の修正とCookie設定のクリアが含まれます。

## 影響を受けるエディションとバージョン：

Adobe Commerceのすべてのバージョンとエディション。

## イシュー

<u>複製する手順</u>:

1. Commerceの管理ページに移動します。
1. 資格情報を入力し、「ログイン」をクリックします。

<u>期待される結果</u>:

Commerce管理者にログインします。

<u>実際の結果</u>:

エラーメッセージなしでログインフォームにリダイレクトされます。

## 原因

この問題の原因として考えられる理由がいくつかあります。

* ブラウザーレベルで設定されたタイムゾーンが正しくありません（実際の有効期間がまだ期限切れになっていなくても、管理者セッションが期限切れと見なされます）。
* Cookie設定が正しくないため、確立されたセッションがAdobe Commerceで使用されません。

それぞれの場合の解決策については、次の段落を参照してください。

## 解決策

### 管理者セッションの有効期間の問題

別のブラウザーを使用し、1時間未満の場合は管理者セッションの有効期間を増やしてみてください。

管理者セッションの有効期間を長くするには、次の手順を実行します。

1. データベースのバックアップを作成します。
1. [phpMyAdmin](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/optional-software#phpmyadmin)などのデータベースツールを使用するか、コマンドラインからDBに手動でアクセスして、次のSQL クエリを実行します。

   ```sql
   UPDATE core_config_data SET value = 7200 WHERE path = 'admin/security/session_lifetime';
   ```

1. 次のコマンドを実行して、設定キャッシュをクリーニングします。

   ```bash
   php <your_magento_install_dir>/bin/magento cache:clean config
   ```

### 不正なCookie設定

Cookie設定の値を確認してクリアするには、次の手順を実行します。

1. データベースのバックアップを作成します。
1. [phpMyAdmin](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/optional-software#phpmyadmin)などのデータベースツールを使用するか、コマンドラインからDBに手動でアクセスして、次のSQL クエリを実行します。

   ```sql
   SELECT * FROM core_config_data WHERE (path = "web/cookie/cookie_domain" OR path = "web/cookie/cookie_path");
   ```

1. 値の応答が空でない場合は、次のコマンドを実行してNULLに設定します。

   ```sql
   UPDATE core_config_data SET value = NULL WHERE (path = "web/cookie/cookie_domain" OR path = "web/cookie/cookie_path");
   ```

1. 次のコマンドを実行して、設定キャッシュをクリーニングします。

   ```bash
   php <your_magento_install_dir>/bin/magento cache:clean config
   ```

## 関連する記事

* [&#x200B; アドビのサポートナレッジベースの「お客様のアカウントは一時的に無効になっています」というエラー](/help/troubleshooting/miscellaneous/redirect-back-to-the-admin-login-form-with-your-account-is-temporarily-disabled-error.md)が表示された場合、管理者ログインフォームにリダイレクトします。
* [管理者ログインフォームにリダイレクトし、サポートナレッジベースの「現在のセッションは期限切れです」というエラー](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-41686)が表示されます。
