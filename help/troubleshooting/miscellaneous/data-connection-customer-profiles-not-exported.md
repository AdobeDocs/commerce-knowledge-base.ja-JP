---
title: Experience Platformに顧客プロファイルが表示されない
description: この記事では、拡張機能の使用時に顧客プロファイルデータがExperience Platformに表示されない場合のトラブルシューティ  [!DNL Data Connection]  グ手順を説明します。
feature: Personalization, Integration, Configuration
role: Admin, Developer
exl-id: 4f12b032-0bee-47da-927a-8d4c2d8b8276
source-git-commit: 1fa5ba91a788351c7a7ce8bc0e826f05c5d98de5
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# Experience Platformに顧客プロファイルが表示されない

この記事では、Data Connection Extension の使用時に顧客プロファイルデータがExperience Platformに表示されない場合のトラブルシューティング手順を説明します。

## 影響を受ける製品とバージョン

* [!DNL Data Connection] extension がインストールされているAdobe Commerce 2.4.x

## 問題

[[!DNL Data Connection]](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/data-connection/overview) 拡張機能をインストールおよび設定し、顧客プロファイルデータをExperience Platformに送信できるようにしたが、そのプロファイルデータがExperience Platformに表示されない。

## 解決策

Experience Platformに顧客プロファイル情報が表示されない場合は、次の点を確認してください。

### 最新バージョンの [!DNL Data Connection] がインストールされていることを確認します

最新バージョンの `experience-platform-connector` 拡張機能がインストールされていることを確認します。

最新バージョンについて詳しくは、[[!DNL Data Connection]  拡張機能リリースノート ](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/data-connection/release-notes) を参照してください。

>[!NOTE]
>
>[!DNL Data Connection] 拡張機能の最新バージョンには、Experience Platformにプロファイルデータを送信する `customers-connector` モジュールが含まれています。 `customers-connector` モジュールはバージョン `1.2.0` 以降である必要があります。

### customers-connector モジュールが設定されていることを確認します。

インストールシナリオに基づいて `customers-connector` モジュールが設定されていることを確認します。

#### クラウドインフラストラクチャー上のAdobe Commerce

1. `.magento.env.yaml` で `ENABLE_EVENTING` グローバル変数を有効にします。 [ 詳細情報 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-global)。

   ```bash
       stage:
           global:
               ENABLE_EVENTING: true
   ```

1. 更新されたファイルをコミットしてクラウド環境にプッシュします。 デプロイメントが完了したら、次のコマンドでイベントの送信を有効にします。

   ```bash
       bin/magento config:set adobe_io_events/eventing/enabled 1
   ```

#### Adobe Commerce オンプレミスでのインストール

コード生成とAdobe Commerce イベントを有効にするには、次のコマンドを実行します。

```bash
   bin/magento events:generate:module
   bin/magento module:enable Magento_AdobeCommerceEvents
   bin/magento setup:upgrade
   bin/magento setup:di:compile
   bin/magento config:set adobe_io_events/eventing/enabled 1
```

### プロファイルデータを取得してExperience Platformに送信できるようにしたことを確認します。

Commerce管理者で、次のフィールドが設定されていることを確認します。

* **[!UICONTROL System]**/**[!UICONTROL Services]**/**[!UICONTROL Data Connection]** で、「[!UICONTROL Back office events]」チェックボックスと「[!UICONTROL Customer profiles]」チェックボックスが有効になっていることを確認します。
* *[!UICONTROL Profile Dataset ID]* フィールドが正しく、行動イベントデータとバックオフィスイベントデータに現在使用しているデータセットとは異なるデータセットであることを確認します。

### イベントがステージング環境または実稼動環境にルーティングされているかどうかを確認

1. 次のコマンドを実行して、現在のAdobe Developer環境を表示します。

   ```bash
   Copy code
   bin/magento config:show
   adobe_io_events/integration/adobe_io_environment
   ```

1. 環境が *[!UICONTROL Stage]* に設定されている場合は、次のコマンドで環境を *[!UICONTROL Production]* に変更します。

   ```bash
   Copy code
   bin/magento config:set adobe_io_events/integration/adobe_io_environment
   production
   ```

### クエリイベントデータの SaaS テーブル

次の [!DNL SQL] クエリに接続して実行し、顧客プロファイルレコードがに表示されることを確認します
テ `event_data_saas` ブルとエラーがないことを確認します。

```sql
Copy code
select * from event_data_saas;
```

### イベント公開エラーの処理

1. 次のエラーが発生した場合は、サンドボックスと実稼動の SaaS コネクタキーが正しいことを確認します。

   ```css
   Copy code
   2024-06-07 14:37:57 | 2024-06-07 14:38:03 | 1 | 0 | Event publishing
   failed: Error code: 403; reason: Forbidden { "error": { "code":
   "Forbidden", "message": "Client ID is invalid", "details": {
   "error_code": "403003" } } }
   ```

1. 管理者の *[!UICONTROL Commerce Services Connector]* ページに移動し、指定した [!UICONTROL sandbox/production] キーが正しく設定されていることを確認します。 また、Commerce アカウントの [!UICONTROL sandbox/production] 設定が、[!UICONTROL Commerce Services Connector] に示す設定と一致することを確認します。 詳細情報 [ 詳細情報 ](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/user-guides/integration-services/saas#apikey)。

### 許可リストにサービス ID が含まれているかどうかを確認し、Adobe Commerce サポートに問い合わせます

1. Adobe Commerceの許可リストに [!UICONTROL Commerce Services Connector] `serviceId` が表示されることを確認します。
1. Adobe Commerceステータスを確認するには、[許可リストに加える サポート ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) にお問い合わせください。

## 関連資料

* Commerce サービスユーザーガイドの [[!DNL Data Connection]](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/data-connection/overview) 拡張機能
* Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
