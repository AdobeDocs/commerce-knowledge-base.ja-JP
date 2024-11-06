---
title: 「クラウドリポジトリ上のAdobe Commerceにアクセスできませんでした：デプロイ中に 403 Forbidden エラーまたは 404 Not Found エラーが発生する」
description: 「この記事では、次のようなクラウドインフラストラクチャー上のAdobe Commerceのデプロイに失敗したというエラーを解決する方法について説明します。」
exl-id: 2f72d80a-05b2-4908-8fa8-61d06885ed07
feature: Cloud, Deploy, Paas, Variables
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 0%

---

# クラウドリポジトリー上のAdobe Commerceにアクセスできませんでした：デプロイ中に「403 Forbidden」または「404 Not Found」エラーが発生する

この記事では、次のような「クラウドインフラストラクチャー上のAdobe Commerceのデプロイメントに失敗しました」エラーを解決する方法について説明します。

「*https://repo.magento.com/archives/magento/magento-cloud-configuration/magento-magento-cloud-configuration-x.x.x.x.zip&#39; URL にアクセスできませんでした：HTTP/1.1 403 Forbidden*」 または、「*https://repo.magento.com/archives/magento/module-customer-segment/magento-module-customer-segment-102.0.5.0-patch2.zip」ファイルをダウンロードできませんでした（HTTP/1.1 404 Not Found）*」。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.2.x、2.3.x および 2.4.x 上のAdobe Commerce

## 問題

リポジトリ URL にアクセスできなかったことを示すデプロイメントのエラーメッセージ。

<u> 再現手順 </u>

トリガーのデプロイメントを手動で行うか、環境の結合、プッシュまたは同期を実行して行います。

<u> 実際の結果 </u>

デプロイメントが停止します。 プロジェクト UI のデプロイメントエラーログに、次のようなエラーメッセージが表示されます。

*「https://repo.magento.com/archives/magento/magento-cloud-configuration/magento-magento-cloud-configuration-x.x.x.x.zip&#39; URL にアクセスできませんでした：HTTP/1.1 \[403 Forbidden or 404 Not Found\]」*。

（ログを確認するには、プロジェクト UI の「失敗」アイコンをクリックします）。

<u> 期待される結果 </u>

デプロイメントが正常に完了しました。

## 原因：

このエラーは、認証キー（アクセス キー）が無効、指定されていない、または正しく指定されていないことが原因です。

キーが無効になる理由には、次のようなものがあります。

* 共有アカウントを使用してキーが生成されました。
* お支払いの問題により、ライセンスは以前に無効になりました。

>[!NOTE]
>
>これが請求または失効の契約の問題が原因である場合は、Adobeアカウントチームにお問い合わせいただき、この問題を解決するためのガイダンスを依頼してください。 ライセンスが再度アクティブ化されると、サポートおよびデプロイメントの使用権限が復元されます。

## 解決策

認証キーの問題を解決するには、次の手順を実行します（各手順の詳細については、以下の節を参照してください）。

1. 有効な認証キーを取得します（キーが有効であることを確実に確認できる場合は、これをスキップします）。
1. `env:COMPOSER_AUTH` 変数にキー値を追加し（または正しい値が存在することを確認し）、プロジェクトレベルおよび環境レベルの変数と、プロジェクトルートの `auth.json` ファイル（存在する場合）でキーの指定が一貫しているかどうかを確認します。
1. 認証キーの値が指定されていない場合や他の値がある場合に、キーが設定されている 1 つの場所のみを使用するように、`auth.json` を更新または削除します。

### 1.有効な認証キーを取得する

共有アカウントで作成したキーを使用していた場合は、アクセス権を付与したAdobe Commerce ライセンスオーナーに連絡し、キーの生成をリクエストする必要があります。

支払いの問題が原因でライセンスが以前に失効され、その問題が解決されてライセンスが更新された場合は、[ 新しい認証キーを生成 ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/authentication-keys.html) する必要があります。

### 2. env:COMPOSER\_AUTH 変数に keys 値を追加し、auth.json で同じキーが指定されているかどうかを確認します

開発者向けドキュメントの [ 既存システムの準備 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/overview) および [ 認証キーの追加 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/overview) の手順と関連情報を参照してください。

### 3. auth.json の更新または削除

次に、認証キーを更新する方法を順を追って説明します。

1. クラウドインフラストラクチャ上にAdobe Commerceがあるマシンに SSH キーでログインします。
1. プロジェクトにログイン：`magento-cloud login`
1. コードを更新するブランチを作成します（次の例では、ブランチ名はプライマリブランチから作成され `auth` す）。     `magento-cloud environment:branch auth master`
1. プロジェクトのルートディレクトリに移動します。
1. オプション：必要に応じて `auth.json` を削除し、[ 手順 9](#step9) に進みます。
1. `auth.json` をテキストエディターで開きます。

   ```json
              {
                "http-basic":  {
                    "repo.magento.com": {
                        "username": "<public_key>",
                        "password": "<private_key>"
                        }
                      }
                    }
   ```

1. 正しい認証キーを追加します。
1. 変更を保存し、テキストエディターを終了します。
1. 変更をコミットしてマージします。

   `git add -A`

   `git commit -m "<message>"`

   `git push origin master`
1. プロジェクトがデプロイされるのを待ちます。
