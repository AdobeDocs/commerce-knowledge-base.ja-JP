---
title: Adobe Commerce *デプロイに失敗したため、デプロイ後にスキップされます* エラー
description: この記事では、デプロイメントエラーを調査する方法について説明します。*デプロイが失敗したため、デプロイ後はスキップされます*
exl-id: cd0a3015-b7b9-442e-8ac1-89447ef12cd7
feature: Deploy
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%
---
# デプロイに失敗したため、Adobe Commerce *デプロイ後にスキップされます* エラー

この記事では、デプロイメントエラーを調査する方法について説明します。例えば、アップグレードなど、異なる環境へのデプロイ中に発生するデプロイが失敗したため、*デプロイ後はスキップされます。*

## 影響を受ける製品とバージョン

クラウドインフラストラクチャ上のAdobe Commerce [&#x200B; サポートされているすべてのバージョン &#x200B;](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## イシュー

デプロイメントが失敗し、一般的なエラーメッセージが返されるため、エラーの解決方法は明確ではありません。

## 原因

未決定 – このエラーメッセージの原因は、デプロイされるコードとデータベースによって異なります。

## デプロイメントエラーの調査方法

```
[20XX-XX-XX XX:XX:XX] DEBUG: Running step: is-deploy-failed
    W:
    W: In Processor.php line 129:
    W:
    [20XX-XX-XX XX:XX:XX] ERROR: [201] Post-deploy is skipped because deploy was failed.
    W:   Post-deploy is skipped because deploy was failed.
    W:
    W:
    W: In DeployFailed.php line 39:
    W:
    W:   Post-deploy is skipped because deploy was failed.
    W:
    W:
    W: post-deploy
    W:
```

実際の原因を特定するためのエラートレースを取得するには、サーバーにSSHで接続し、ログファイル `var/log/install_upgrade.log`を確認します。
