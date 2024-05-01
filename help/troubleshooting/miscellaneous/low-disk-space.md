---
title: ディスク容量が少ない
description: ここでは、クラウドインフラストラクチャー上のAdobe Commerceの特定の環境で容量が不足した場合の解決策について説明します。
exl-id: 1b2c25d3-ca1b-4409-8d6b-378aa0952f94
feature: Storage, Observability
role: Developer
source-git-commit: 9ee4145d5516a37fab1c092d539000627f242a93
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# ディスク容量が少ない

ここでは、クラウドインフラストラクチャー上のAdobe Commerceの特定の環境で容量が不足した場合の解決策について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべて [サポートされているバージョン](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

## 問題

書き込み可能なディレクトリを持つディスクのディスク領域が不足しています。 症状の 1 つに以下のものがあります。 [デプロイメントの停止](/help/troubleshooting/deployment/deployment-stuck-with-unable-to-upload-the-application-to-the-remote-cluster-error.md).

ディスク使用量を確認するには、次のコマンドを実行します。

```bash
df -h var/
```

## 原因：

この `var` ディレクトリは通常、多くのスペースを取ることができ、簡単に掃除することができます。

Adobe Commerceは、すべてのログファイルをに保存します。 `var` ディレクトリ。 新しいログファイルが作成され、古いログファイルが毎日アーカイブされます。 ただし、生成されるエラーの数が増え続ける場合は、ログファイルにより多くの容量が必要になります。

カスタムのインポート/エクスポートファイルも以下に保存されます。 `var` ディレクトリ、およびその数が増加した場合はスペースを取る。

## 解決策

ソリューションオプション：

* 大きなログファイルがあるかどうかを確認し、それが大きい理由を調査して、大量のログ出力を生成する問題を修正します。
* を掃除する `var` ディレクトリ。
* のサイズを追跡する cron ジョブを設定 `var` ディレクトリを削除してクリーンアップします。
* 未使用のディスク容量がある場合は、割り当てるディスク容量を増やします。 （スペース制限を確認する方法については、以下の節を参照してください）。
   * スタータープラン、すべての環境、および Pro プラン統合環境の場合、の説明に従って、未使用のディスク容量があれば割り当てることができます [ディスク領域の管理：ディスク領域の割り当て](https://devdocs.magento.com/guides/v2.3/cloud/project/manage-disk-space.html#application-disk-space).
   * Pro プランのステージング環境および実稼動環境では、未使用のディスク容量がある場合に割り当てるディスク容量を増やすには、サポートにお問い合わせください。
* ディスク容量の上限に達してもディスク容量の不足が発生する場合は、ディスク容量の購入を検討してください。詳しくは、Adobeアカウントチームにお問い合わせください。

### ディスク容量の制限を確認

クラウドインフラストラクチャ環境の各Adobe Commerceに空き容量を確認するには、次の手順を実行します。

1. にログインします [クラウドコンソール](https://console.adobecommerce.com).
1. 日 **[!UICONTROL All projects]** ダッシュボードで、関連するプロジェクトを選択します。 左隅に、空きディスク容量が表示されます。

   ![project_space.png](/help/troubleshooting/miscellaneous/assets/project_space.png)
