---
title: Cloud UIに「ログスニップ」エラーがある場合のデプロイメントログの確認
description: この記事では、クラウドプロジェクト UIでデプロイメントログを表示しようとすると、Adobe Commerce on cloud infrastructure UIに「長すぎるためログが切り取られました」というエラーメッセージが表示される問題の解決策を紹介します。
exl-id: 04d28741-72c1-4722-be46-425fe136b9a6
feature: Cloud, Deploy, Logs, Paas
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: 3c398179-d35a-51ba-b317-6c5b95feef5e
    internal-label: Logs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%
---
# クラウド UIに&#x200B;*ログが抜き取られた* エラーがある場合のデプロイメントログの確認

この記事では、クラウドプロジェクト UIでデプロイメントログを表示しようとすると、「*ログが長すぎる*」というエラーメッセージが表示されるAdobe Commerce オンクラウドインフラストラクチャ UIで発生する問題の解決策を紹介します。 （[Adobe Commerce Cloud Console](https://console.adobecommerce.com/)には適用されません）。

## 影響を受ける製品

Adobe Commerce オンクラウドインフラストラクチャ（サポートされているすべてのバージョン）

## イシュー

クラウドプロジェクト UIでデプロイメントログを表示しようとすると、クラウドインフラストラクチャ UI上のAdobe Commerceに次のエラーメッセージが表示されます。*ログが長すぎたため無視されました*。

## 再生の手順

1. プロジェクト URLに移動し、該当するデプロイメントの&#x200B;**ステータス**&#x200B;をクリックします。
1. ログが長すぎてUIに表示されない場合、エラーメッセージが表示されます。*長すぎたためログが切り取られました*。

## 原因

UIに表示されるログは、信頼できる唯一の情報源として扱ってはなりません。特に、デプロイメントが「成功」のステータスで表示された後にサイトが応答していないか、正しく動作していないことがわかっている場合は、注意してください。 サーバー上のログでも確認する必要があります。 開発者ドキュメントの[&#x200B; ログの表示と管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html)を参照してください。

## Solution

1. ローカル環境に[Magento Cloud CLI](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/cloud-cli.html)がインストールされていることを確認してください。
1. 次のいずれかのコマンドを実行できます。

   ```bash
   magento-cloud act -p <project id> -e <environment>
   ```

   ```bash
   magento-cloud activity:list -p <project id> -e <environment>
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

1. 影響を受けるデプロイメントのアクティビティ IDをコピーし、次のコマンドを実行します。

   ```bash
   magento-cloud activity:log <activity ID> -p <project id> -e <environment>
   ```

   失敗したデプロイメントのログを調べる例：

   ```bash
   magento-cloud activity:log raah5xrhqz3wg -p <project id> -e <environment>
   ```

## 開発者向けドキュメントの関連情報：

* [Adobe Commerce on cloud infrastructure > ビルドとデプロイ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/configure-env-yaml.html)
* [Adobe Commerce クラウドインフラストラクチャ/ログの表示と管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html)
