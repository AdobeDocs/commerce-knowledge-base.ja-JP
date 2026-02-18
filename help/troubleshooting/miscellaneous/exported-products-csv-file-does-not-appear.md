---
title: 書き出された製品の.csv ファイルが表示されない
description: ここでは、Commerce Admin で目的のエンティティタイプを.csv ファイルに書き出そうとしても、ファイルが表示されない問題の解決策を説明します。
exl-id: 8e3bb65c-ea75-4af4-ad4b-4d94ab219bbb
feature: Cache, Data Import/Export, Products, Variables
role: Developer
source-git-commit: da2df5fc4ab6cc10d86af806045ee884b01f291d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# 書き出された製品の.csv ファイルが表示されない

ここでは、目的のエンティティタイプをCommerce Admin の.csv ファイルに書き出すとファイルが表示されない問題の解決策について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべて [&#x200B; サポート対象バージョン &#x200B;](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)。

## 問題

<u> 再現手順 </u>

前提条件：「**URL への秘密鍵の追加**」オプションが *はい* に設定されている。 このオプションは、Commerce管理者の **ストア**/**設定**/**詳細**/**管理者**/**セキュリティ** で設定されています。

1. 管理者で、**システム**/**データ転送**/**書き出し** に移動します。

   ![magento_export_products_2.3.4.png](assets/magento_export_products_2.3.4.png)

1. を選択
   * **エンティティタイプ**：書き出すエンティティ
   * **書き出しファイル形式**: *CSV*
   * **フィールド エンクロージャ**：オフのままにします。
1. **続行** をクリックします。
1. *「メッセージがキューに追加されました。すぐにファイルを取得するまで待ってください」* というメッセージが表示されます。

<u> 期待される結果 </u>

エクスポートされた目的のエンティティタイプを含む.csv ファイルが、数分以内にグリッドに表示されます。

<u> 実際の結果 </u>

エクスポートされた目的のエンティティタイプを含む.csv ファイルが、10 分以上でグリッドに表示されません。

## 原因：

Adobe Commerce アプリケーション部分バージョン 2.3.2 の書き出し機能に関する既知の問題。

## 解決策

この問題には、次の 2 つの解決策が考えられます。

* 「URL に秘密鍵を追加」オプションを無効にします。
* `bin/magento queue:consumers:start exportProcessor` コマンドを手動で実行し、必要に応じて cron で実行するように設定します。

以降の段落で、両方のオプションの詳細を参照してください。

### 「URL に秘密鍵を追加」オプションを無効にします

1. 管理者で、**ストア**/**設定**/**詳細**/**管理者**/**セキュリティ** に移動します。
1. 「**秘密鍵を URL に追加**」オプションを *いいえ* に設定します。
1. 「**設定を保存**」をクリックします。
1. **システム**/**ツール**/**キャッシュ管理** の下で、または    管理者で、またはを ```bash    bin/magento cache:clean``` きます。

### export コマンドを手動で実行し、オプションで cron ジョブとして追加します。

エクスポートファイルを取得するには、`bin/magento queue:consumers:start exportProcessor` コマンドを実行します。 これを実行すると、ファイルがグリッドに表示されます。


プロセスを cron ジョブとしてオプションで追加するには、`CRON_CONSUMERS` 変数を `.magento.env.yaml` ファイルに追加する必要があります。

#### Cron ジョブとしてのプロセスの追加（オプション）

1. Cron が設定され、設定されていることを確認します。 詳しくは [cron ジョブの設定 &#x200B;](/docs/commerce-cloud-service/user-guide/configure/app/properties/crons-property.html) を参照してください。
1. 次のコマンドを実行して、メッセージキューコンシューマーのリストを返します。     `./bin/magento queue:consumers:list`
1. ルートアプリケーションディレクトリの `.magento.env.yaml` ファイルに次のコードを追加し、追加するコンシューマーを含めます。 例えば、エクスポート処理に必要な消費者を次に示します。

   ```yaml
   stage:
       deploy:
           CRON_CONSUMERS_RUNNER:
               cron_run: true
               max_messages: 1000
               consumers:
                   - exportProcessor
   ```

   次に、この更新されたファイルをプッシュし、環境を再デプロイします。 また、開発者向けドキュメントの [&#x200B; プロジェクトへのカスタム cron ジョブの追加 &#x200B;](/docs/commerce-cloud-service/user-guide/configure/app/properties/crons-property.html#add-custom-cron-jobs-to-your-project) も参照してください。

>[!NOTE]
>
>環境用の `.magento.env.yaml` ファイルが見つからず、削除されたと思われる場合は、新しい `.magento.env.yaml` を作成する必要があります。 最初は空の場合がありますが、必要に応じて情報を追加できます。 アドビの開発者ドキュメントの [&#x200B; デプロイメント用の環境変数の設定 &#x200B;](/docs/commerce-cloud-service/user-guide/configure/env/configure-env-yaml.html) および [&#x200B; 環境変数 &#x200B;](/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-intro.html) の記事を参照してください。

>[!TIP]
>
>[YAML ファイル &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/configure-env-yaml.html) では大文字と小文字が区別され、タブは使用できません。 .magento.env.yaml ファイル全体で一貫したインデントを使用するように注意してください。使用しないと、設定が期待どおりに動作しない場合があります。 ドキュメントとサンプルファイルの例では、2 つのスペースのインデントを使用しています。 ece-tools validate コマンドを使用して、設定を確認します。

>[!NOTE]
>
>Cloud infrastructure Pro プロジェクトのAdobe Commerceでは、[&#x200B; を使用してステージング環境と実稼動環境にカスタム cron ジョブを追加する前に、クラウドインフラストラクチャのAdobe Commerceで &#x200B;](/docs/commerce-cloud-service/user-guide/configure/app/properties/crons-property.html?lang=en#crontab) 自動クローン機能 `.magento.app.yaml` を有効にする必要があります。 この機能が有効になっていない場合は、[&#x200B; サポートチケットを作成 &#x200B;](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket) して、ジョブを追加します。
