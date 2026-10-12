---
title: デプロイメントエラー：* エラー7がポート 443をダウンロード中に発生しました：接続が拒否されました*
description: この記事では、デプロイメントエラーの解決策を提供します。*「ダウンロード中にエラー7... ポート 443：接続が拒否されました」*。
exl-id: 520cf50f-3682-441d-87a7-8e05301a2b0c
feature: Cache, Deploy
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: b673188e-f9fa-492a-b470-c8f949bf7827
    internal-label: Cache
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%
---
# 展開エラー：*ダウンロード中にエラー7が発生しました… ポート 443：接続が拒否されました*

この記事では、デプロイメントが次のエラーメッセージで失敗した場合の問題の修正について説明します。

```bash
W: In CurlDownloader.php line 370:
W:
W:   curl error 7 while downloading https://repo.packagist.org/p2/magento/module
W:   -sitemap.json: Failed to connect to repo.packagist.org port 443: Connection
W:    refused
```

## 影響のあるバージョン

クラウドインフラストラクチャ上のAdobe Commerce、[&#x200B; サポートされているすべてのバージョン &#x200B;](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## イシュー

展開が失敗し、**curl エラー7** メッセージが表示されます。

<u>複製する手順</u>:

トリガーとデプロイメント：

<u>期待される動作</u>:

デプロイが成功しました。

<u>実際の動作</u>:

デプロイメントが失敗し、次のエラーが発生しました：*curl error 7 while downloading ... port 443：接続が拒否されました* appears in the deploy log.

## 原因

これは、リポジトリに対するキャッシュ接続が失われた可能性があります。

## Solution

プロジェクトのスーパーユーザーに次のコマンドを実行するように依頼します。

```bash
magento-cloud project:clear-build-cache -p <project ID>
```

プロジェクトの誰がスーパーユーザーであるかを確認するには、「Commerce on Cloud Infrastructure ガイド」の「[&#x200B; ユーザーのプロジェクトロールを表示](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html?lang=en#view-a-user's-project-role)」を参照してください。

## 関連リソース

* [Adobe Commerce デプロイメントのトラブルシューティング &#x200B;](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-29640)。
* [&#x200B; クラウドリポジトリ上のAdobe Commerceにアクセスできませんでした：403 Forbiddenまたは404 Not Found エラー（デプロイ時） &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-commerce-cloud-repo-could-not-be-accessed-403-forbidden-or-404-not-found-error-when-deploying.html)。
* [&#x200B; デプロイメントが「プロジェクトの構築エラー：構築フックがステータスコード 1で失敗しました」 &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/deployment/deployment-fails-with-error-building-project-the-build-hook-failed-with-status-code-1.html)で失敗しました。
