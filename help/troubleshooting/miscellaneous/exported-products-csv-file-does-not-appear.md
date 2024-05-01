---
title: 書き出された製品の.csv ファイルが表示されない
description: ここでは、Commerce Admin で商品を.csv ファイルに書き出そうとした際に、ファイルが表示されない問題の解決策を説明します。
exl-id: 8e3bb65c-ea75-4af4-ad4b-4d94ab219bbb
feature: Cache, Data Import/Export, Products, Variables
role: Developer
source-git-commit: 465eb89cf5c5169b0b459ab7e6bdcbd418781093
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# 書き出された製品の.csv ファイルが表示されない

ここでは、Commerce Admin で商品を.csv ファイルに書き出そうとした際に、ファイルが表示されない問題の解決策を説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべて [サポートされているバージョン](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf).

## 問題

<u>再現手順</u>

前提条件：次の **URL への秘密鍵の追加** オプションの設定 *はい*. このオプションは、の下のCommerce管理で設定されます。 **ストア** > **設定** > **詳細** > **Admin** > **セキュリティ**.

1. 管理者で、に移動します。 **システム** > **データ転送** > **Export**.

   ![magento_export_products_2.3.4.png](assets/magento_export_products_2.3.4.png)

1. を選択
   * **エンティティタイプ**: *製品*
   * **書き出しファイル形式**: *CSV*
   * **フィールド格納装置**：オフのままにします。
1. クリック **続行**.
1. 次のメッセージが表示されます。 *「メッセージがキューに追加されました。すぐにファイルを取得するのを待ってください」*.

<u>期待される結果</u>

書き出された製品を含む.csv ファイルが、数分でグリッドに表示されます。

<u>実際の結果</u>

エクスポートされた製品を含む.csv ファイルが 10 分以上でグリッドに表示されません。

## 原因：

Adobe Commerce アプリケーション部分バージョン 2.3.2 の書き出し機能に関する既知の問題。

## 解決策

この問題には、次の 2 つの解決策が考えられます。

* 「URL に秘密鍵を追加」オプションを無効にします。
* を実行 `bin/magento queue:consumers:start exportProcessor` 手動でコマンドを実行し、必要に応じて cron で実行するように設定します。

以降の段落で、両方のオプションの詳細を参照してください。

### 「URL に秘密鍵を追加」オプションを無効にします

1. 管理者で、に移動します。 **ストア** > **設定** > **詳細** > **Admin** > **セキュリティ**.
1. を **URL への秘密鍵の追加** 対するオプション *いいえ。*
1. クリック **設定を保存**.
1. の下のキャッシュをクリーンアップ **システム** > **ツール** > **キャッシュ管理** または走ることによって    ```bash    bin/magento cache:clean``` または管理で確認できます。

### export コマンドを手動で実行し、オプションで cron ジョブとして追加します。

エクスポートファイルを取得するには、次を実行します `bin/magento queue:consumers:start exportProcessor` コマンド。 これを実行すると、ファイルがグリッドに表示されます。


プロセスを cron ジョブとしてオプションで追加するには、 `CRON_CONSUMERS` 変数を `.magento.env.yaml` ファイル。

#### Cron ジョブとしてのプロセスの追加（オプション）

1. Cron が設定され、設定されていることを確認します。 参照： [cron ジョブの設定](/docs/commerce-cloud-service/user-guide/configure/app/properties/crons-property.html) を参照してください。
1. 次のコマンドを実行して、メッセージキューコンシューマーのリストを返します。     `./bin/magento queue:consumers:list`
1. 以下のを `.magento.env.yaml` ファイルをルートアプリケーションディレクトリに追加し、追加するコンシューマーを含めます。 例えば、エクスポート処理に必要な消費者を次に示します。

   ```yaml
   stage:
       deploy:
           CRON_CONSUMERS_RUNNER:
               cron_run: true
               max_messages: 1000
               consumers:
                   - exportProcessor
   ```

   次に、この更新されたファイルをプッシュし、環境を再デプロイします。 も参照 [プロジェクトへのカスタム cron ジョブの追加](/docs/commerce-cloud-service/user-guide/configure/app/properties/crons-property.html#add-custom-cron-jobs-to-your-project) 開発者向けドキュメントを参照してください。

>[!NOTE]
>
>が見つからない場合は、 `.magento.env.yaml` 環境用のファイルですが、削除されたと思われる場合は、新しく作成する必要があります `.magento.env.yaml`. 最初は空の場合がありますが、必要に応じて情報を追加できます。 次の記事を参照してください。 [デプロイメント用の環境変数の設定](/docs/commerce-cloud-service/user-guide/configure/env/configure-env-yaml.html) および [環境変数](/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-intro.html) 開発者向けドキュメントを参照してください。

>[!NOTE]
>
>Cloud infrastructure Pro プロジェクトのAdobe Commerceでは、 [オートクロン機能](/docs/commerce-cloud-service/user-guide/configure/app/properties/crons-property.html?lang=en#crontab) を使用してステージング環境と実稼動環境にカスタム cron ジョブを追加するには、まずクラウドインフラストラクチャ上のAdobe Commerceで有効にする必要があります `.magento.app.yaml`. この機能が有効になっていない場合、 [サポートチケットを作成](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)：ジョブを追加します。
