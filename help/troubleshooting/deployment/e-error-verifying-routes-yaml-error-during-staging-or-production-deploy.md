---
title: 「E：ステージングまたは実稼動デプロイ中に routes.yaml エラーを検証中にエラーが発生しました」
description: '「この記事では、クラウドインフラストラクチャー上のAdobe Commerceの問題に対して、プロジェクトをステージング環境または実稼動環境にデプロイしようとすると、「*E: Error while verifying routes.yaml」*というエラーメッセージが表示される解決策を提供します。」'
exl-id: 7f58591a-5581-46cd-984d-09ac2c0f3903
feature: Deploy, Routes, Staging
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# E：ステージングデプロイまたは実稼動デプロイ中の routes.yaml エラーの検証エラー

この記事では、プロジェクトをステージング環境または実稼動環境にデプロイしようとすると、*「E: Error while verifying routes.yaml」* というエラーメッセージが表示されるクラウドインフラストラクチャー上のAdobe Commerceの問題に対するソリューションを説明します。

## 影響を受けるバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン

## 問題

<u> 再現手順 </u>:

コードをステージング環境または実稼動環境にプッシュして、デプロイをトリガーします。

<u> 想定される動作 </u>:

デプロイメントに成功しました。

<u> 実際の動作 </u>:

デプロイメントがブロックされ、次のエラーメッセージがログに表示されます。

<pre>アプリケーションのデプロイ設定の確認 E: routes.yaml の検証中にエラーが発生しました。
以下のドメインがクラスターに設定されていますが、routes.yaml ファイルでルートが定義されていません。

- store1.example.com
- store2.example.com
- test-store.example.com

現在の routes.yaml 設定を使用すると、
  これらのドメインは提供されません。

続行するには、こちらを参照してトラブルシューティング手順を確認してください。
 /help/troubleshooting/deployment/e-error-verifying-routes-yaml-error-during-staging-or-production-deploy.md</pre>

## 原因：

このエラーは、プロジェクトに追加された追加ドメインのルート設定が `routes.yaml` ファイルにない場合に発生します。

セルフサービスルート設定用のAdobe Commerce セルフサービス有効化アップグレードの一環として、プロジェクト内のすべてのドメインの `routes.yaml` ファイルにルートが設定されていることを確認するデプロイ前のチェックを追加しました。 ルート設定がないドメインがある場合、デプロイメントはブロックされます。

## 解決策

ブロックされたデプロイメントを解決するには、次のいずれかの方法を使用して、エラーメッセージにリストされているドメインのルートを設定するように `routes.yaml` ファイルを更新します。

* アップグレードプロセス中に、Adobe Commerceから提供されたパッチを適用します。
* 見つからないルート設定を `routes.yaml` ファイルに手動で追加します。

### 方法 1:Adobe Commerceから提供されたパッチを適用する

1. 「*&lt;project\_ID> のセルフサービス機能を有効にする」というタイトルの付いた最新のAdobe Commerce サポートチケットを探し* す。
1. チケットの指示に従ってパッチを適用します。これにより、クラウド環境のルート設定が更新されます。
1. 変更сコミットしてプッシュし、プロジェクトを再デプロイします。

### 方法 2：見つからないルート設定を手動で追加する

1. プロジェクト内のすべてのドメインを同じルート設定を使用して提供するには、次の例に示すように、デフォルトのドメインとプロジェクト内のその他すべてのドメインのルートテンプレートを追加して、`routes.yaml` ファイルを更新します。

   ```yaml
   "http://{default}/":
       type: upstream
       upstream: "mymagento:http"
   "http://{all}/":
       type: upstream
       upstream: "mymagento:http"
   ```

1. с変更をコミットし、プッシュしてプロジェクトを再デプロイします。

ルート設定を更新する詳細な手順については、開発者向けドキュメントの [Cloud for Adobe Commerce/ルートの設定 ](https://devdocs.magento.com/guides/v2.3/cloud/project/project-conf-files_routes.html) を参照してください。

>[!NOTE]
>
>プロジェクトの設定で、使用されなくなったドメインが指定されている場合は、次の手順を実行して、できるだけ早い時期にプロジェクトからドメインを削除します。1. プロジェクト環境から削除するドメインのリストを含んだサポートチケットを送信します。 2. サポートチームがドメインを削除したら、`routes.yaml` ファイルを更新して、古いドメインへの参照をすべて削除します。
