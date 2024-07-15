---
title: Cloud UI に「ログのスニペット」エラーがあるかどうかをデプロイメントログで確認しています
description: この記事では、クラウドプロジェクト UI でデプロイメントログを表示しようとすると、「長すぎたので、Adobe Commerceでログが切り抜かれました」というエラーメッセージが表示される問題の解決策を説明します。
exl-id: 04d28741-72c1-4722-be46-425fe136b9a6
feature: Cloud, Deploy, Logs, Paas
role: Developer
source-git-commit: 71bec5b99063d771982f6dcab111b9e5a4aaec69
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# クラウド UI に *log snipped* エラーがあるかどうかをデプロイメントログで確認しています

この記事では、クラウドプロジェクト UI でデプロイメントログを表示しようとすると、クラウドインフラストラクチャ UI のAdobe Commerceで *ログのスニペットが長すぎるので* というエラーメッセージが表示される問題の解決策について説明します。 （[Adobe Commerce Cloud コンソール ](https://console.adobecommerce.com/) には適用されません。）

## 対象製品

クラウドインフラストラクチャー上のAdobe Commerce（サポート対象のすべてのバージョン）

## 問題

クラウドプロジェクト UI でデプロイメントログを表示しようとすると、クラウドインフラストラクチャ UI 上のAdobe Commerceに、「*ログが長すぎるので切り抜かれました* というエラーメッセージが表示されます。

## 再現手順

1. プロジェクト URL に移動し、該当するデプロイメントの **ステータス** をクリックします。
1. ログが長すぎて UI に表示できない場合は、「*ログが長すぎるのでスニペットされました*」というエラーメッセージが表示されます。

## 原因：

UI に表示されるログは、特に、デプロイメントが成功ステータスでリストされた後、サイトが応答しないか、正しく動作していないことが判明した場合には、信頼できるソースとして扱わないでください。 また、サーバー上のログでも確認する必要があります。 開発者向けドキュメントの [ ログの表示と管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html) を参照してください。

## 解決策

1. ローカル環境に [Magentoの Cloud CLI](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/cloud-cli.html) がインストールされていることを確認します。
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

* [ クラウドインフラストラクチャー上のAdobe Commerce/ビルドとデプロイ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/configure-env-yaml.html)
* [ クラウドインフラストラクチャー上のAdobe Commerce/ログの表示と管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html)
