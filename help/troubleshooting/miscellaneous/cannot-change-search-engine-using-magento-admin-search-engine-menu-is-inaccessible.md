---
title: Commerce Admin を使用して検索エンジンを変更できない（検索エンジンメニューにアクセスできない）
description: この記事では、「検索エンジン」フィールドが表示されない場合や、「システム値を使用」チェックボックスが灰色表示になっておりアクセスできない場合に、Commerce管理者を使用してAdobe Commerce検索エンジンを変更するための解決策を提供します。
exl-id: 5b0f728c-6a8d-446d-9553-5abc3d01e516
feature: Admin Workspace, Search, Variables
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 0%

---

# Commerce Admin を使用して検索エンジンを変更できない（検索エンジンメニューにアクセスできない）

>[!WARNING]
>
> [MySQL カタログ検索エンジンは、Adobe Commerce 2.4.0 で削除されます](/help/announcements/adobe-commerce-announcements/mysql-catalog-search-engine-will-be-removed-in-magento-2-4-0.md). バージョン 2.4.0 をインストールする前に、Elasticsearch・ホストをセットアップして構成する必要があります。こちらを参照してください [Elasticsearchのインストールと設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/elasticsearch.html).

この記事では、次の場合にCommerce Admin を使用してAdobe Commerce検索エンジンを変更するソリューションを提供します **検索エンジン** フィールドが表示されない **システム値を使用** チェックボックスが灰色表示になっており、アクセスできません。

この記事の内容は次のとおりです。

* [影響を受けるバージョン](#affected-versions)
* [Commerce Admin を使用した検索エンジンの変更（手順）](#change-search-engine-using-magento-admin-steps)
* [Adobe Commerceのオンプレミスにおける問題）](#magento-commerce-on-premise)
* [クラウドインフラストラクチャー上のAdobe Commerce](#magento-commerce-cloud)

## 影響を受けるバージョン

* Adobe Commerce オンプレミス：2.X.X
* クラウドインフラストラクチャー上のAdobe Commerce:
   * バージョン：2.X.X
   * スターターおよび Pro プランアーキテクチャ
* MySQL、Elasticsearch：サポートされているすべてのバージョン

## 管理者を使用して検索エンジンを変更する（手順）

1. 管理者として「Admin」にログインします。
1. 左側の管理サイドバーで、 **ストア**. 次に、の下に **設定**、を選択 **設定**.
1. の下にある左側のパネル **カタログ、** を選択 **カタログ**.
1. を展開します。 **カタログ検索** セクション。    ![catalog_menu.png](assets/catalog_menu.png)
1. に移動します **検索エンジン** フィールドに移動し、から選択を削除します **システム値を使用** チェックボックス。
1. 「」をクリックします **検索エンジン** メニューをクリックし、使用可能なオプションの 1 つを選択します。    ![search_engine_menu.png](assets/search_engine_menu.png)
1. クリック **設定を保存** ページの右上隅

## Adobe Commerceのオンプレミスにおける問題

### 問題 1：検索エンジンフィールドが表示されない

にアクセスした場合 **カタログ検索** セクション、 **検索エンジン** メニューがまったく表示されない。

![search_engine_not_displayed.png](assets/search_engine_not_displayed.png)

### 原因：ストア ビューが既定の構成ではありません

管理者のストア表示が以外の値に設定されています。 *デフォルトの設定*.

検索エンジンは、ストア範囲ではなく、アプリケーションレベルで設定されるグローバル設定です。 Adobe Commerce アプリケーション内のストアは、異なる検索エンジンを使用できません。

### 解決策：ストア表示をデフォルト設定に設定します

1. 管理者として「Admin」にログインします。
1. 左側の管理サイドバーで、 **ストア**. 次に、の下に **設定**、を選択 **設定**.
1. 左上隅のをクリックします **ストア表示** セレクターと選択 *デフォルトの設定*.
1. クリック **OK** 確認ダイアログで「ストア表示の変更を承認」を選択します。

![change_store_view.png](assets/change_store_view.png)

**関連ドキュメント：** [範囲の変更](https://experienceleague.adobe.com/docs/commerce-admin/config/scope-change.html#set-the-scope) を参照してください。

### 問題 2:「システム値を使用」をオフにできません

にアクセスした場合 **カタログ検索** 管理者セクション、 **システム値を使用** チェックボックスがグレー表示になっているので、選択をチェックボックスから削除して後で検索エンジンを変更することはできません。

### 原因：

デフォルトの検索エンジンは、 `app/etc/env.php` または `app/etc/config.php` ファイルはなので、管理者を使用して変更できません。

デフォルトの検索エンジン設定を含むセクションの例：

```php
'system'=>
array (
'default'=>
array (
'catalog'=>
array (
'search'=>
array (
'engine'=>'mysql',
),
),
),
),
```

### 解決策

デフォルトの検索エンジン設定を使用して「」セクションをから削除します `app/etc/env.php` または `app/etc/config.php` 設定ファイル。

### 開発者向けドキュメントの関連記事

[Adobe Commerce設定ファイル](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/deployment-files.html) （Adobe Commerce設定ガイド）

## クラウドインフラストラクチャー上のAdobe Commerce

クラウドインフラストラクチャの編成の仕方により、クラウドインフラストラクチャ上のAdobe Commerceでは、管理者を使用して検索エンジンを切り替えることはできません。

デプロイメントプロセス中に、クラウドインフラストラクチャー上のAdobe Commerce デプロイメントスクリプトは、でElasticsearchが宣言されているかどうかを確認します。 `MAGENTO_CLOUD_RELATIONSHIPS` 変数。 宣言すると、Elasticsearchがアクティブな検索エンジンとして選択され、自動的に設定されます。 [MySQL 検索エンジン](/help/announcements/adobe-commerce-announcements/mysql-catalog-search-engine-will-be-removed-in-magento-2-4-0.md) 管理者でアクセスできなくなります。 Elasticsearch関係が宣言されていない場合、MySQL はアクティブに設定され、Elasticsearchにアクセスできなくなります。

を編集することはお勧めしません `app/etc/env.php` または `app/etc/config.php` 設定ファイルをクラウド環境に直接配置します。そのため、これらのファイルを変更してElasticsearchエンジンを管理者に表示するソリューション（前の節で推奨したソリューション）は、クラウドプロジェクトには適用されません。

### ステージング環境と実稼動環境での検索エンジンの変更

ステージング環境と実稼動環境で検索エンジンを MySQL からElasticsearchに切り替える前に、必ず以前に設定しておいてください [がサポートチケットを送信しました](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) 環境とチケットのElasticsearchの有効化のリクエストが正常に解決されました。

ステージング環境と実稼動環境で使用する検索エンジンを変更するには、 `SEARCH_CONFIGURATION` の環境変数 `.magento.env.yaml` ローカル環境にを置いてから、変更を統合環境およびステージング環境/実稼動環境にプッシュして、変更を有効にします。

MySQL からElasticsearchに切り替えた場合、SEARCH\_CONFIGURATION 変数は結果として `.magento.env.yaml` ファイルは次のようになります。

```yaml
stage:
  deploy:
   SEARCH_CONFIGURATION:
     engine: elasticsearch
     elasticsearch_server_hostname: hostname
     elasticsearch_server_port: '123456'
     elasticsearch_index_prefix: magento
     elasticsearch_server_timeout: '15'
```

### 関連ドキュメント

#### サポートナレッジベース

* [クラウドでElasticsearchを有効にする](/help/how-to/general/enable-elasticsearch-on-cloud.md)

#### 開発者向けドキュメント

* [Elasticsearchサービスの設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/elasticsearch.html)
* [ビルドとデプロイ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/configure-env-yaml.html) （ドキュメントについて） `.magento.env.yaml` 設定ファイル）
* [変数のデプロイ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html) （[SEARCH\_CONFIGURATION セクション](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html#search_configuration)）
* [サービス](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/services-yaml.html) （ドキュメントについて） `.magento/services.yaml` 設定ファイル）
