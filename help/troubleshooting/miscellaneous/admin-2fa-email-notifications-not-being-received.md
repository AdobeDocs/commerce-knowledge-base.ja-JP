---
title: 管理者 2FA のメール通知を受信できない
description: この記事では、クラウドインフラストラクチャ上のAdobe Commerceで管理者アクセスセキュリティを強化するために、二要素認証（2FA）を設定した後、設定完了の手順が記載されたメールが届かない場合のトラブルシューティングについて説明します。
exl-id: 7ab6b2b4-6aca-4323-a45b-2b4e52955160
feature: Admin Workspace, Communications
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---

# 管理者 2FA のメール通知を受信できない


## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン

## 問題

管理者アクセスのセキュリティを強化するために 2 要素認証を設定しましたが、設定の完了手順が記載されたメールが届きません。

## 原因：

送信者メールを適切に設定していない場合、またはドメインが SendGrid でホワイトレーベル付けされていない場合、メールはスパムフォルダーに入っていた可能性があります。

## トラブルシューティング

### 手順 1：スパムフォルダーを確認する

1. メールがスパムフォルダーに表示されなかった場合は、この Mysql クエリを実行して、メールアドレスが設定されていることを確認します。

   ```sql
   select * from core_config_data where path like '%trans_email%';
   ```

   * 結果が返されない場合は、送信者アドレスが設定されていないことを意味します。
管理者へのアクセス権がないので、設定をデータベースに挿入する必要があります。 適切なメールアドレスを差し込み、MySQL 文を実行します。

   ```
   insert into core_config_data (scope,scope_id,path,value) values ('default',0,'trans_email/ident_general/email', your-email@here.com)
   ```

   * 結果が返された場合は、**手順 2** に進みます。

1. メールがスパムフォルダーに表示された場合は、メール内のリンクをクリックします。 リンクの有効期限が切れてから再度ログインして、このプロセスを繰り返します。
1. アクセス権を取得したら、**ストア**/**設定**/**一般**/**メールアドレスを保存** に移動してメールアドレスを設定します。

### 手順 2：メールアドレスが正しく設定されている場合は、環境に SSH で接続し、次のコマンドを実行します。

```php
php -r "mail(<your email address>,<subject>,<content>,'To: <sender email>');"
```

メールのスパムフォルダーを確認します。 メールが表示された場合は、[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#login)、SendGrid でドメインにホワイトレーベルが付くようリクエストします。

## 関連資料

* 開発者向けドキュメントの [SendGrid](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/project/sendgrid)。
