---
title: Cloud UI に「ログのスニペット」エラーがあるかどうかをデプロイメントログで確認しています
description: この記事では、デプロイメントログを表示しようとすると、Adobe Commerce on cloud infrastructure UI で「長すぎたので、ログが切り抜かれました」というエラーメッセージが表示される問題の解決策を説明します。
exl-id: 04d28741-72c1-4722-be46-425fe136b9a6
feature: Cloud, Deploy, Logs, Paas
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Cloud UI に「ログのスニペット」エラーがあるかどうかをデプロイメントログで確認しています

この記事では、クラウドインフラストラクチャ UI 上のAdobe Commerceでが表示される問題の解決策について説明します *長すぎるためログが切り取られました* デプロイメントログを表示しようとすると、エラーメッセージが表示されます。

## 対象製品

クラウドインフラストラクチャー上のAdobe Commerce（サポート対象のすべてのバージョン）

## 問題

デプロイメントログを表示しようとすると、クラウドインフラストラクチャ UI 上のAdobe Commerceに次のエラーメッセージが表示されます。 *長すぎるためログが切り取られました*.

## 再現手順

1. プロジェクト URL に移動し、 **ステータス** 対象のデプロイメントの。
1. ログが長すぎて UI に表示されない場合は、次のエラーメッセージが表示されます。 *長すぎるためログが切り取られました*.

## 原因：

UI に表示されるログは、特に、デプロイメントが成功ステータスでリストされた後、サイトが応答しないか、正しく動作していないことが判明した場合には、信頼できるソースとして扱わないでください。 また、サーバー上のログでも確認する必要があります。 こちらを参照してください [ログの表示と管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html) 開発者向けドキュメントを参照してください。

## 解決策

1. 次が揃っていることを確認します [MagentoCloud CLI](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/cloud-cli.html) ローカル環境にインストールされていること。
1. 次のコマンドを実行します。

   ```bash
   magento-cloud activity -p <project id> -e <environment>
   ```

1. 次のような出力が返されます。

   ```bash
   Activities on the project <project name> (project id), environment <environment>:
   +---------------+---------------------------+-------------------------------------+----------+----------+---------+
   | ID            | Created                   | Description                         | Progress | State    | Result  |
   +---------------+---------------------------+-------------------------------------+----------+----------+---------+
   | l5wgwmzwrsskg | 2021-06-01T08:18:02-07:00 | ABC merged Integration into Staging | 100%     | complete | success |
   | raah5xrhqz3wg | 2021-06-01T08:07:18-07:00 | XYZ pushed to Integration           | 100%     | complete | failure |
   ```

1. 影響を受けるデプロイメントのアクティビティ ID をコピーし、次のコマンドを実行します。

   ```bash
   magento-cloud activity:log <activity ID> -p <project id> -e <environment>
   ```

   失敗したデプロイメントのログを確認する例：

   ```bash
   magento-cloud activity:log raah5xrhqz3wg -p <project id> -e <environment>
   ```

## 開発者向けドキュメントの関連する読み値：

* [クラウドインフラストラクチャー上のAdobe Commerce/ビルドとデプロイ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/configure-env-yaml.html)
* [クラウドインフラストラクチャー上のAdobe Commerce/ログの表示と管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html)
