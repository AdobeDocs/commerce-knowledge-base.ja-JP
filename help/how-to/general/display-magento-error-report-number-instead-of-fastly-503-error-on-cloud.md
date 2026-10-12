---
title: Fastly 503 エラーではなくAdobe Commerce エラーレポート番号を表示
description: デフォルトでは、Fastlyは「**503 Service Unavailable**」エラーの背後にあるすべてのAdobe Commerce エラーを非表示にします。 Adobe Commerce エラーログレポート番号を表示するには（ログでエラーログを確認し、エラーの詳細を確認するには）、次の手順を使用してFastlyを省略するweb サイトを開きます。
exl-id: c0a4a9f8-a674-4cef-8088-e844594e6076
feature: Cache, Cloud
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: b673188e-f9fa-492a-b470-c8f949bf7827
    internal-label: Cache
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%
---
# Fastly 503 エラーではなくAdobe Commerce エラーレポート番号を表示

デフォルトでは、Fastlyは&#x200B;**503 Service Unavailable** エラーの背後にあるすべてのAdobe Commerce エラーを非表示にします。 Adobe Commerce エラーログレポート番号を表示するには（ログでエラーログを確認し、エラーの詳細を確認するには）、次の手順を使用してFastlyを省略するweb サイトを開きます。

1. アプリケーションのドメインとIP アドレスをローカルマシン上のhosts ファイルに追加します。
1. ブラウザーのキャッシュとCookieを消去します（またはシークレットモードに切り替えます）。
1. ストアのweb サイトを再度開き、Adobe Commerce エラーを確認します。

Authentic Adobe Commerce エラーとエラーレポート番号が表示されたら、次の手順に従ってエラーレポートファイルの詳細を確認できます。

1. 影響を受ける環境へのSSH。 開発者ドキュメントの[環境へのSSH](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections)を参照してください。
1. `./var/report/{error_number}` ファイルを探します。

## アプリケーションドメインとIP アドレスをhosts ファイルに追加する：詳細な手順

1. ローカルマシンのコマンドラインで`nslookup` コマンドを実行して、ストアのサーバーIPを確認します。
   * プロアーキテクチャユーザー（ステージング環境および実稼動環境）:

   ```
   nslookup {your_project_id}.ent.magento.cloud
   ```

   * スターターアーキテクチャユーザー（すべての環境）、プロアーキテクチャユーザー（統合環境）:

   ```
   nslookup gw.{your_region}.magentosite.cloud
   ```

1. 次の形式を使用して、ストアドメインとアプリケーションサーバーのIPをローカルマシン上のhosts ファイルに追加します。

```
{server_IP} {store_domain}
```
