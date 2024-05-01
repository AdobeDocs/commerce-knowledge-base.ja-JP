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

この記事では、クラウドインフラストラクチャー上のAdobe Commerceの問題に対して、次のような解決策を提供します *「E:routes.yaml の検証中にエラーが発生しました」* プロジェクトをステージング環境または実稼動環境にデプロイしようとすると、エラーメッセージが表示されます。

## 影響を受けるバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン

## 問題

<u>再現手順</u>:

コードをステージング環境または実稼動環境にプッシュして、デプロイをトリガーします。

<u>予期される動作</u>:

デプロイメントに成功しました。

<u>実際の動作</u>:

デプロイメントがブロックされ、次のエラーメッセージがログに表示されます。

<pre>アプリケーションのデプロイ設定の確認 E: routes.yaml の検証中にエラーが発生しました。
クラスターに次のドメインが設定されていますが、routes.yaml ファイルでルートが定義されていません：- store1.example.com - store2.example.com - test-store.example.com現在の routes.yaml 設定では、これらのドメインは提供されません。

続行するには、トラブルシューティングの手順を次の場所で確認してください：/help/troubleshooting/deployment/e-error-verifying-routes-yaml-error-during-staging-or-production-deploy.md</pre>

## 原因：

このエラーは、プロジェクトに追加された追加ドメインのルート設定が `routes.yaml` ファイル。

セルフサービスルート設定用のAdobe Commerce セルフサービス有効化アップグレードの一環として、プロジェクト内のすべてのドメインがでルートが設定されていることを確認するデプロイ前のチェックを追加しました `routes.yaml` ファイル。 ルート設定がないドメインがある場合、デプロイメントはブロックされます。

## 解決策

ブロックされたデプロイメントを解決するには、 `routes.yaml` 次のいずれかの方法を使用して、エラーメッセージにリストされているドメインのルートを設定するためのファイル：

* アップグレードプロセス中に、Adobe Commerceから提供されたパッチを適用します。
* 不足しているルート設定をに手動で追加する `routes.yaml` ファイル。

### 方法 1:Adobe Commerceから提供されたパッチを適用する

1. 「」というタイトルの最近のAdobe Commerce サポートチケットを探します&#x200B;*のセルフサービス機能を有効にする &lt;project _id=&quot;&quot;>」と入力します。*
1. チケットの指示に従ってパッチを適用します。これにより、クラウド環境のルート設定が更新されます。
1. 変更сコミットしてプッシュし、プロジェクトを再デプロイします。

### 方法 2：見つからないルート設定を手動で追加する

1. 同じルート設定を使用してプロジェクト内のすべてのドメインを提供するには、 `routes.yaml` 次の例に示すように、デフォルトのドメインおよびプロジェクト上のその他すべてのドメインのルートテンプレートを追加するファイル。

   ```yaml
   "http://{default}/":
       type: upstream
       upstream: "mymagento:http"
   "http://{all}/":
       type: upstream
       upstream: "mymagento:http"
   ```

1. с変更をコミットし、プッシュしてプロジェクトを再デプロイします。

ルート設定を更新する詳細な手順については、を参照してください [Cloud for Adobe Commerce/ルートを設定](https://devdocs.magento.com/guides/v2.3/cloud/project/project-conf-files_routes.html) 開発者向けドキュメントを参照してください。

>[!NOTE]
>
>プロジェクトの設定で、使用されなくなったドメインが指定されている場合は、次の手順を実行して、できるだけ早い時期にプロジェクトからドメインを削除します。1. プロジェクト環境から削除するドメインのリストを含んだサポートチケットを送信します。 2. サポートチームがドメインを削除したら、 `routes.yaml` 古いドメインへの参照を削除するファイル。
