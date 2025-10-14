---
title: ディスク容量が少ない
description: ここでは、クラウドインフラストラクチャー上のAdobe Commerceの特定の環境で容量が不足した場合の解決策について説明します。
exl-id: 1b2c25d3-ca1b-4409-8d6b-378aa0952f94
feature: Storage, Observability
role: Developer
source-git-commit: 842c329b5d8bacf72ac689412fde5a5d76d16e85
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---

# ディスク容量が少ない

ここでは、クラウドインフラストラクチャー上のAdobe Commerceの特定の環境で容量が不足した場合の解決策について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべて [&#x200B; サポート対象バージョン &#x200B;](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

## 問題

書き込み可能なディレクトリを持つディスクのディスク領域が不足しています。 症状の 1 つに、デプロイメントが停止 [&#x200B; することがあります &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26878)。

ディスク使用量を確認するには、次のコマンドを実行します。

```bash
df -h var/
```

## 原因：

`var` ディレクトリは、通常、多くのスペースを取ることができ、簡単に消去できるディレクトリです。

Adobe Commerceでは、すべてのログファイルが `var` ディレクトリに格納されます。 新しいログファイルが作成され、古いログファイルが毎日アーカイブされます。 ただし、生成されるエラーの数が増え続ける場合は、ログファイルにより多くの容量が必要になります。

カスタムのインポート/エクスポートファイルも `var` ディレクトリに格納され、ファイルの数が増えるとスペースを取ります。

## 解決策

ソリューションオプション：

* 大きなログファイルがあるかどうかを確認し、それが大きい理由を調査して、大量のログ出力を生成する問題を修正します。
* `var` ディレクトリをクリーンアップします。
* `var` ディレクトリのサイズを追跡してクリーンアップする cron ジョブを設定します。
* 未使用のディスク容量がある場合は、割り当てるディスク容量を増やします。 （スペース制限を確認する方法については、以下の節を参照してください）。
   * スタータープラン、すべての環境、Pro プラン統合環境の場合は、[&#x200B; ディスク領域の管理：ディスク領域の割り当て &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space#application-disk-space) で説明しているように、未使用のディスク領域があれば割り当てることができます。
   * Pro プランのステージング環境および実稼動環境では、未使用のディスク容量がある場合に割り当てるディスク容量を増やすには、サポートにお問い合わせください。
* スペースの制限に達してもスペースの問題が発生する場合は、ディスク容量の購入を検討してください。詳しくは、Adobe アカウントチームにお問い合わせください。

### ディスク容量の制限を確認

クラウドインフラストラクチャ環境の各Adobe Commerceに空き容量を確認するには、次の手順を実行します。

1. [Cloud Console](https://console.adobecommerce.com) にログインします。
1. **[!UICONTROL All projects]** ダッシュボードで、関連するプロジェクトを選択します。 左隅に、空きディスク容量が表示されます。

   ![project_space.png](/help/troubleshooting/miscellaneous/assets/project_space.png)
