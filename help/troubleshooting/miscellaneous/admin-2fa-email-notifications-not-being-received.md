---
title: 管理者 2FA のメール通知を受信できない
description: この記事では、クラウドインフラストラクチャ上のAdobe Commerceで管理者アクセスセキュリティを強化するために、二要素認証（2FA）を設定した後、設定完了の手順が記載されたメールが届かない場合のトラブルシューティングについて説明します。
exl-id: 7ab6b2b4-6aca-4323-a45b-2b4e52955160
feature: Admin Workspace, Communications
role: Developer
source-git-commit: 9eaea028886e74fc06c9516801919cd7f650f98c
workflow-type: tm+mt
source-wordcount: '449'
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

メールのスパムフォルダーを確認します。

メールがスパムフォルダーに表示された場合、ドメインのメール認証が SendGrid 経由の送信配信用に完全に設定されていない可能性があります。

Adobeが管理する SendGrid サービスを使用している場合：

[ サポートチケットを送信 ](https://experienceleague.adobe.com/home?support-tab=home#support)SendGrid で送信ドメインを認証（または *ホワイトレーベル*）するようにリクエストします。
このプロセスには、ドメインに代わってメールを送信するように SendGrid を認証する DNS レコード（DKIMと SPF）を追加することが含まれます。これにより、メールがスパムフォルダーではなくインボックスに配信される可能性が高まります。

独自の SendGrid アカウントを使用している場合：

SendGrid アカウントダッシュボード内でドメイン認証設定を直接管理する責任があります。 詳しくは、SendGrid ドキュメントの [ ドメイン認証の設定方法 ](https://www.twilio.com/docs/sendgrid/ui/account-and-settings/how-to-set-up-domain-authentication) を参照してください。

>[!NOTE]
>
>一部のお客様は、メールの配信品質とコンプライアンス（HIPAA 要件など）を完全に制御するために、個別にプロビジョニングされた SendGrid サービスを使用する場合があります。 使用している SendGrid サービスのタイプ（Adobe管理と自己管理）に応じた正しいトラブルシューティング手順に従っていることを確認します。


## 関連資料

* 開発者向けドキュメントの [SendGrid](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/sendgrid)。
