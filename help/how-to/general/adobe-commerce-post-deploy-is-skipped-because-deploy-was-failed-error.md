---
title: Adobe Commerceの*デプロイに失敗したので*デプロイ後の*エラーはスキップされます
description: 「この記事では、デプロイメントエラーを調査する方法を説明します。*デプロイに失敗したので、Post-deploy はスキップされます*」
exl-id: cd0a3015-b7b9-442e-8ac1-89447ef12cd7
feature: Deploy
source-git-commit: 83b21845cd306336e1cb193a9541478c8a38eea8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# Adobe Commerce *デプロイに失敗したので、デプロイ後はスキップされます* エラー

この記事では、デプロイメントエラーを調査する方法を説明します。*アップグレードなど* 様々な環境へのデプロイメント中にデプロイが失敗したので、Post-deploy はスキップされます。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce[&#x200B; サポート対象のすべてのバージョン &#x200B;](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## 問題

デプロイメントが失敗し、一般的なエラーメッセージが返されるので、エラーの解決方法が不明です。

## 原因：

未確定 – このエラーメッセージが表示される原因は、デプロイされているコードとデータベースによって異なります。

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

実際の原因を特定するためのエラートレースを取得するには、サーバーに SSH で接続し、ログファイルの `var/log/install_upgrade.log` を確認します。
