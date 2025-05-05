---
title: Commerce Admin にログインしようとすると、ログインリダイレクトが発生する
description: この記事では、管理者にログインしようとするとログインフォームにリダイレクトされ、エラーメッセージが表示されない、Commerceの管理者ログインの問題に対する解決策を説明します。 これには、サーバーのタイムゾーン設定の修正や、Adobe Commerceでの cookie 設定のクリアが含まれます。
exl-id: ff3114fd-8690-4983-8221-cf807f083b15
feature: Admin Workspace, Cache
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Commerce Admin にログインしようとすると、ログインリダイレクトが発生する

この記事では、管理者にログインしようとするとログインフォームにリダイレクトされ、エラーメッセージが表示されない、Commerceの管理者ログインの問題に対する解決策を説明します。 これには、サーバーのタイムゾーン設定の修正や、Adobe Commerceでの cookie 設定のクリアが含まれます。

## 影響を受けるエディションとバージョン：

Adobe Commerceのすべてのバージョンとエディション。

## 問題

<u> 再現手順 </u>:

1. Commerce管理者ページに移動します。
1. 資格情報を入力し、「ログイン」をクリックします。

<u> 期待される結果 </u>:

Commerce管理者にログインします。

<u> 実際の結果 </u>:

エラーメッセージを表示せずにログインフォームにリダイレクトされます。

## 原因：

この問題には、次のような理由が考えられます。

* ブラウザーレベルで間違ったタイムゾーンが設定されています（これにより、実際の有効期限がまだ切れていない場合でも、管理セッションが期限切れと見なされます）。
* Cookie の設定が正しくないので、確立済みセッションがAdobe Commerceで使用されません。

それぞれの場合の解決策については、次の段落を参照してください。

## 解決策

### 管理セッションの有効期間の問題

別のブラウザーを使用し、1 時間未満の場合は管理セッションの有効期間を増やしてみてください。

管理者セッションの有効期間を延長するには、次の手順に従います。

1. データベースバックアップを作成します。
1. [phpMyAdmin](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/optional-software#phpmyadmin) などのデータベースツールを使用するか、コマンドラインから手動で DB にアクセスして、次の SQL クエリを実行します。

   ```sql
   UPDATE core_config_data SET value = 7200 WHERE path = 'admin/security/session_lifetime';
   ```

1. 次のコマンドを実行して、設定キャッシュをクリーンアップします。

   ```bash
   php <your_magento_install_dir>/bin/magento cache:clean config
   ```

### Cookie の設定が正しくない

Cookie の設定値を確認してクリアするには、次の手順に従います。

1. データベースバックアップを作成します。
1. [phpMyAdmin](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/optional-software#phpmyadmin) などのデータベースツールを使用するか、コマンドラインから手動で DB にアクセスして、次の SQL クエリを実行します。

   ```sql
   SELECT * FROM core_config_data WHERE (path = "web/cookie/cookie_domain" OR path = "web/cookie/cookie_path");
   ```

1. 値の応答が空でない場合は、次のコマンドを実行して NULL に設定します。

   ```sql
   UPDATE core_config_data SET value = NULL WHERE (path = "web/cookie/cookie_domain" OR path = "web/cookie/cookie_path");
   ```

1. 次のコマンドを実行して、設定キャッシュをクリーンアップします。

   ```bash
   php <your_magento_install_dir>/bin/magento cache:clean config
   ```

## 関連記事

* サポートナレッジベースで [ 「アカウントが一時的に無効になっています」というエラーが表示されて ](/help/troubleshooting/miscellaneous/redirect-back-to-the-admin-login-form-with-your-account-is-temporarily-disabled-error.md) 管理者ログインフォームにリダイレクトし直します。
* サポートナレッジベースで [ 「現在のセッションは期限切れです」というエラーが表示された管理者ログインフォームにリダイレクトし ](/help/troubleshooting/miscellaneous/redirect-back-to-the-admin-login-form-with-your-current-session-has-been-expired-error.md) す。
