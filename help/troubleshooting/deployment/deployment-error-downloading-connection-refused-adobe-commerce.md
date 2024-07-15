---
title: 「デプロイメントエラー：*.. ポート 443 のダウンロード中にエラー 7 が発生する：接続が拒否されました*」
description: '「この記事では、デプロイメントエラーの解決策を説明します。*"error 7 while downloading ... port 443: Connection refused"*.'''
exl-id: 520cf50f-3682-441d-87a7-8e05301a2b0c
feature: Cache, Deploy
role: Developer
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# 展開エラー：*ダウンロード中のエラー 7... ポート 443：接続が拒否されました*

この記事では、次のエラーメッセージでデプロイメントが失敗した場合の問題の修正について説明します。

```bash
W: In CurlDownloader.php line 370:
W:
W:   curl error 7 while downloading https://repo.packagist.org/p2/magento/module
W:   -sitemap.json: Failed to connect to repo.packagist.org port 443: Connection
W:    refused
```

## 影響を受けるバージョン

クラウドインフラストラクチャー上のAdobe Commerce[ サポート対象のすべてのバージョン ](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## 問題

デプロイメントが失敗し、**curl エラー 7** メッセージが表示されます。

<u> 再現手順 </u>:

デプロイメントをトリガーします。

<u> 想定される動作 </u>:

デプロイメントに成功しました。

<u> 実際の動作 </u>:

デプロイが失敗し、「*ダウンロード中の curl エラー 7... ポート 443：接続が拒否されました*」というエラーがデプロイログに表示されます。

## 原因：

これは、リポジトリへのキャッシュ接続が失われることが原因である可能性があります。

## 解決策

プロジェクトのスーパーユーザーに、次のコマンドを実行するように依頼します。

```bash
magento-cloud project:clear-build-cache -p <project ID>
```

Commerce プロジェクトの誰がスーパーユーザーかを確認するには、『 Cloud Infrastructure ガイド』の [ ユーザーのプロジェクトの役割を表示 ](/docs/commerce-cloud-service/user-guide/project/user-access.html?lang=en#view-a-user’s-project-role) を参照してください。

## 推奨読み取り

* [Adobe Commerce デプロイメントのトラブルシューティング ](/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-deployment-troubleshooter.html)。
* [cloud repo のAdobe Commerceにアクセスできませんでした：デプロイ中に 403 Forbidden エラーまたは 404 Not Found エラーが発生しました ](/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-commerce-cloud-repo-could-not-be-accessed-403-forbidden-or-404-not-found-error-when-deploying.html)。
* [ 「プロジェクトの構築エラー：ビルドフックがステータスコード 1 で失敗しました」でデプロイメントが失敗します ](/docs/commerce-knowledge-base/kb/troubleshooting/deployment/deployment-fails-with-error-building-project-the-build-hook-failed-with-status-code-1.html)。
