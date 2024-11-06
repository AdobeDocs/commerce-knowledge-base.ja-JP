---
title: Fastly 503 エラーの代わりにAdobe Commerce エラーレポート番号を表示
description: 「デフォルトでは、Fastly は、**503 サービスを利用できません**エラーの背後にあるすべてのAdobe Commerce エラーを非表示にします。 Adobe Commerce エラーログレポート番号を表示するには（ログで見つけてエラーの詳細を確認できるようにするには）、次の手順に従って、Fastly を省略して web サイトを開きます。'
exl-id: c0a4a9f8-a674-4cef-8088-e844594e6076
feature: Cache, Cloud
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Fastly 503 エラーの代わりにAdobe Commerce エラーレポート番号を表示

デフォルトでは、Fastly は、**503 Service Unavailable** エラーの背後にあるすべてのAdobe Commerce エラーを非表示にします。 Adobe Commerce エラーログレポート番号を表示するには（ログで見つけて、エラーの詳細を確認できるようにするには）、次の手順に従って、Fastly を省略して web サイトを開きます。

1. ローカルマシン上の hosts ファイルにアプリケーションのドメインと IP アドレスを追加します。
1. ブラウザーのキャッシュと Cookie をクリアします（または匿名モードに切り替えます）。
1. ストアの web サイトを再度開いて、Adobe Commerce エラーを確認します。

authentic Adobe Commerce エラーとエラーレポート番号が表示されたら、次の手順に従って、エラーレポートファイルで詳細を取得できます：

1. 影響を受ける環境に SSH で接続します。 開発者向けドキュメントの [ 環境への SSH](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections) を参照してください。
1. `./var/report/{error_number}` ファイルを見つけます。

## ホストファイルへのアプリケーションドメインと IP アドレスの追加：詳細な手順

1. ローカルマシンのコマンドラインで `nslookup` コマンドを実行して、ストアのサーバー IP を確認します。
   * Pro アーキテクチャユーザー（ステージング環境と実稼動環境）:

   ```
   nslookup {your_project_id}.ent.magento.cloud
   ```

   * スターターアーキテクチャユーザー（すべての環境）、Pro アーキテクチャユーザー（統合環境）:

   ```
   nslookup gw.{your_region}.magentosite.cloud
   ```

1. 次の形式を使用して、ストアドメインとアプリケーションサーバーの IP をローカルマシン上の hosts ファイルに追加します。

```
{server_IP} {store_domain}
```
