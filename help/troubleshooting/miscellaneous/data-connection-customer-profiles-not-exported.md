---
title: Experience Platformに顧客プロファイルが表示されない
description: この記事では、 [!DNL Data Connection] 拡張機能を使用する際に、お客様のプロファイルデータがExperience Platformに表示されない場合のトラブルシューティング手順について説明します。
feature: Personalization, Integration, Configuration
role: Admin, Developer
exl-id: 4f12b032-0bee-47da-927a-8d4c2d8b8276
source-git-commit: 1fa5ba91a788351c7a7ce8bc0e826f05c5d98de5
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---

# Experience Platformに顧客プロファイルが表示されない

この記事では、Data Connection拡張機能を使用する際に、お客様のプロファイルデータがExperience Platformに表示されない場合のトラブルシューティング手順について説明します。

## 影響を受ける製品とバージョン

* 拡張機能[!DNL Data Connection]がインストールされたAdobe Commerce 2.4.x

## イシュー

拡張機能[[!DNL Data Connection]](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/data-connection/overview)をインストールして設定し、お客様のプロファイルデータをExperience Platformに送信することを有効にしましたが、そのプロファイルデータはExperience Platformに表示されません。

## Solution

お客様のプロフィール情報がExperience Platformに表示されない場合は、次の点を確認してください。

### 最新バージョンの[!DNL Data Connection]がインストールされていることを確認してください

最新バージョンの`experience-platform-connector`拡張機能がインストールされていることを確認してください。

最新バージョンについて詳しくは、[[!DNL Data Connection] 拡張機能リリースノート ](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/data-connection/release-notes)を参照してください。

>[!NOTE]
>
>[!DNL Data Connection]拡張機能の最新バージョンには、`customers-connector` モジュールが含まれています。このモジュールは、Experience Platformにプロファイルデータを送信する役割を担っています。 `customers-connector` モジュールはバージョン `1.2.0`以降である必要があります。

### customers-connector モジュールが設定されていることを確認します

インストール シナリオに基づいて`customers-connector` モジュールが設定されていることを確認します。

#### Adobe Commerce on Cloud インフラストラクチャ

1. `.magento.env.yaml`で`ENABLE_EVENTING` グローバル変数を有効にします。 [学習を増やす](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-global)。

   ```bash
       stage:
           global:
               ENABLE_EVENTING: true
   ```

1. 更新されたファイルをコミットしてクラウド環境にプッシュします。 デプロイメントが完了したら、次のコマンドを使用してイベントの送信を有効にします。

   ```bash
       bin/magento config:set adobe_io_events/eventing/enabled 1
   ```

#### Adobe Commerce オンプレミスのインストール

コード生成とAdobe Commerce Eventsを有効にするには、次のコマンドを実行します。

```bash
   bin/magento events:generate:module
   bin/magento module:enable Magento_AdobeCommerceEvents
   bin/magento setup:upgrade
   bin/magento setup:di:compile
   bin/magento config:set adobe_io_events/eventing/enabled 1
```

### プロファイルデータのキャプチャとExperience Platformへの送信を有効にしていることを確認します

Commerce管理者で、次のフィールドが設定されていることを確認します。

* **[!UICONTROL System]** > **[!UICONTROL Services]** > **[!UICONTROL Data Connection]**&#x200B;で、[!UICONTROL Back office events]と[!UICONTROL Customer profiles]のチェックボックスが有効になっていることを確認します。
* *[!UICONTROL Profile Dataset ID]* フィールドが正しく、現在の行動およびバックオフィスのイベントデータに使用しているデータセットとは異なるデータセットであることを確認してください。

### イベントがステージングまたは実稼動環境にルーティングされているかどうかを確認します

1. 次のコマンドを実行して、現在のAdobe Developer環境を表示します。

   ```bash
   Copy code
   bin/magento config:show
   adobe_io_events/integration/adobe_io_environment
   ```

1. 環境が&#x200B;*[!UICONTROL Stage]*&#x200B;に設定されている場合は、次のコマンドで&#x200B;*[!UICONTROL Production]*&#x200B;に変更します。

   ```bash
   Copy code
   bin/magento config:set adobe_io_events/integration/adobe_io_environment
   production
   ```

### クエリイベントデータ SaaS テーブル

次の[!DNL SQL] クエリを接続して実行し、顧客プロファイルレコードが
`event_data_saas` テーブルとエラーがないことを確認します：

```sql
Copy code
select * from event_data_saas;
```

### イベント公開エラーの処理

1. 次のエラーが発生した場合は、サンドボックスと実稼動SaaS コネクタキーが正しいことを確認してください。

   ```css
   Copy code
   2024-06-07 14:37:57 | 2024-06-07 14:38:03 | 1 | 0 | Event publishing
   failed: Error code: 403; reason: Forbidden { "error": { "code":
   "Forbidden", "message": "Client ID is invalid", "details": {
   "error_code": "403003" } } }
   ```

1. 管理者の&#x200B;*[!UICONTROL Commerce Services Connector]* ページに移動し、指定した[!UICONTROL sandbox/production] キーが正しく設定されていることを確認します。 また、Commerce アカウント [!UICONTROL sandbox/production]の設定が[!UICONTROL Commerce Services Connector]に表示されている設定と一致していることを確認します。 [詳細](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/user-guides/integration-services/saas#apikey)を学習します。

### サービス IDが許可リストにあるかどうかを確認し、Adobe Commerce サポートに確認します

1. [!UICONTROL Commerce Services Connector] `serviceId`がAdobe Commerceの許可リストに表示されていることを確認します。
1. [Adobe Commerce サポート ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)にお問い合わせいただき、ステータスを確認してください。

## 関連トピックス

* Commerce Services ユーザーガイドの[[!DNL Data Connection]](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/data-connection/overview)拡張機能
* [Commerce実装プレイブックのデータベーステーブルを修正するためのベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
