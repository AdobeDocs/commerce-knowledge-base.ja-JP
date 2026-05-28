---
title: 管理者2FAのメール通知が受信されない
description: この記事では、Adobe Commerceのクラウドインフラストラクチャでの管理者アクセスのセキュリティを強化するために、2要素認証（2FA）を設定した後に、設定完了手順に関するメールが届かない場合のトラブルシューティングについて説明します。
exl-id: 7ab6b2b4-6aca-4323-a45b-2b4e52955160
feature: Admin Workspace, Communications
role: Developer
source-git-commit: 9eaea028886e74fc06c9516801919cd7f650f98c
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# 管理者2FAのメール通知が受信されない


## 影響を受ける製品とバージョン

* Adobe Commerceオンクラウドインフラストラクチャ（全バージョン）

## イシュー

管理者アクセスのセキュリティを強化するために2要素認証を設定しましたが、設定の完了に関する説明が記載されたメールは受信されません。

## 原因

送信者の電子メールが適切に設定されていない場合、またはドメインがSendGridでホワイトラベル化されていない場合、電子メールは迷惑メールフォルダーに送信される可能性があります。

## トラブルシューティング

### ステップ 1：迷惑メールフォルダーを確認する

1. 電子メールが迷惑メールフォルダーに表示されない場合は、次のMysql クエリを実行して、電子メールアドレスが設定されていることを確認します。

   ```sql
   select * from core_config_data where path like '%trans_email%';
   ```

   * 結果が返されない場合は、送信者アドレスが設定されていないことを意味します。
管理者にアクセスできないので、設定をデータベースに挿入する必要があります。 適切なメールアドレスを接続し、MySQL ステートメントを実行します。

   ```
   insert into core_config_data (scope,scope_id,path,value) values ('default',0,'trans_email/ident_general/email', your-email@here.com)
   ```

   * 結果を返す場合は、**手順2**&#x200B;に進みます。

1. 電子メールが迷惑メールフォルダーに表示された場合は、電子メール内のリンクをクリックします。 リンクの有効期限が切れた後は、再度ログインしてプロセスを繰り返してください。
1. アクセス権を取得したら、**ストア** > **設定** > **一般** > **電子メールアドレスを保存**&#x200B;に移動し、電子メールアドレスを設定します。

### ステップ 2：電子メールアドレスが正しく設定されたら、環境にSSHで接続し、次のコマンドを実行します。

```php
php -r "mail(<your email address>,<subject>,<content>,'To: <sender email>');"
```

電子メールの迷惑メールフォルダーを確認します。

電子メールが迷惑メールフォルダーに表示された場合、ドメインの電子メール認証がSendGridを介したアウトバウンド配信用に完全に設定されていない可能性があります。

Adobeが管理するSendGrid サービスを使用している場合：

SendGridで送信ドメインを認証することを要求する[ サポートチケット ](https://experienceleague.adobe.com/home?support-tab=home#support)を送信します（*ホワイトラベル*と呼ばれることもあります）。
このプロセスでは、DNS レコード（DKIMとSPF）を追加して、SendGridがドメインの代理でメールを送信することを許可します。これにより、迷惑メールフォルダーではなく受信トレイにメールが配信される可能性が高まります。

自分のSendGrid アカウントを使用している場合：

お客様は、SendGrid アカウントダッシュボード内でドメイン認証設定を直接管理する責任があります。 詳しくは、SendGrid ドキュメントの[ ドメイン認証の設定方法](https://www.twilio.com/docs/sendgrid/ui/account-and-settings/how-to-set-up-domain-authentication)を参照してください。

>[!NOTE]
>
>一部のお客様は、電子メールの配信品質とコンプライアンスの完全な制御（HIPAA要件など）のために、個別にプロビジョニングされたSendGrid サービスを使用することを選択する場合があります。 使用しているSendGrid サービスの種類（Adobe管理サービスとセルフマネージドサービス）に基づいて、正しいトラブルシューティング手順に従っていることを確認します。


## 関連トピックス

* 開発者ドキュメントの[SendGrid](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/sendgrid)。
