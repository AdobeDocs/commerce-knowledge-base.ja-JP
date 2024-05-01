---
title: ストアのフロントカタログページでログに「整合性制約違反」が記録され、503 エラーが発生する
description: この記事では、ストアフロントカタログページにアクセスできないことに関連する、cloud infrastructure 2.2.0 上の既知のAdobe Commerceの問題に対するパッチを提供します。
exl-id: ad363744-756a-48b9-ae11-58642e0ca6a4
feature: Catalog Management, Logs
role: Developer
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# ストアのフロントカタログページでログに「整合性制約違反」が記録され、503 エラーが発生する

>[!NOTE]
>
>この記事では、回避策としてパッチを提供しますが、この問題は cloud infrastructure v2.3.3 リリースのAdobe Commerceで永続的に修正されており、v2.3.3 にアップグレードすることをお勧めします。の手順に従います [Adobe Commerceのバージョンのアップグレード](https://devdocs.magento.com/cloud/project/project-upgrade.html) 開発者向けドキュメントを参照してください。

この記事では、ストアフロントカタログページにアクセスできず、「ログイン」ログに次のようなエラーメッセージが表示される、cloud infrastructure 2.2.0 上の既知のAdobe Commerceの問題に対するパッチを提供します。 *整合性制約違反：1062 キー&#39;プライマリ&#39;の重複エントリ &#39;%entry%&#39;、クエリ：INSERT INTO \&#39;search\_tmp\_%number%*.

## 問題

ストア フロント カタログ ページに予期せずアクセスできなくなります。 エラーログには、次のようなエラー説明が含まれます。 *整合性制約違反：1062 キー&#39;プライマリ&#39;の重複エントリ &#39;%entry%&#39;、クエリ：INSERT INTO \&#39;search\_tmp\_%number%*.

この問題は検索に関連しており、インデックス再作成後に新しいインデックスとともに古いインデックスが存在することが原因です。

## 解決策

この問題を修正するには、Elasticsearchから古いインデックスを削除し、表示されないようにパッチを適用する必要があります。

すべてのインデックスをリストするには、次のコマンドを使用します。

<pre>curl -X GET %elasticsearch_domain%:%elasticsearch_port%/_cat/indices</pre>

古いインデックスを削除するには、データベース内でインデックスを見つけて、次のコマンドを使用します。

```bash
curl -X DELETE %elasticsearch_domain%:%elasticsearch_port%/%product_id%_v%outdated_version%
```

例：

```bash
curl -X DELETE 127.0.0.1:9200/magento2_product_8_v332
```

## パッチ

パッチはこの記事に添付されています。 パッチをダウンロードするには、記事の最後までスクロールして必要なファイル名をクリックするか、次のリンクのいずれかをクリックします。

[MDVA-9590\_EE\_2.2.0\_COMPOSER\_v2.patch のダウンロード](assets/MDVA-9590_EE_2.2.0_COMPOSER_v2.patch.zip)

[MDVA-13203\_EE\_2.2.4\_V1\_COMPOSER.patch のダウンロード](assets/MDVA-13203_EE_2.2.4_V1_COMPOSER.patch.zip)

## 互換性のあるAdobe Commerce バージョン

パッチは、次のエディションとバージョン用に作成されました。

* クラウドインフラストラクチャー 2.2.0 上のAdobe Commerce（`MDVA-9590_EE_2.2.0_COMPOSER_v2.patch`）
* クラウドインフラストラクチャー 2.2.4 上のAdobe Commerce（`MDVA-13203_EE_2.2.4_V1_COMPOSER.patch`）

この `MDVA-9590_EE_2.2.0_COMPOSER_v2` patch は、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決する可能性があります）。

* cloud infrastructure 2.0.X、2.1.X、2.2.X、および 2.3.0 ～ 2.3.3 のAdobe Commerce
* Adobe Commerce オンプレミス 2.0.X、2.1.X、2.2.X、および 2.3.0 ～ 2.3.3

この `MDVA-13203_EE_2.2.4_V1_COMPOSER` patch は、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決する可能性があります）。

* cloud infrastructure 2.0.X、2.1.X、2.2.X、および 2.3.0 ～ 2.3.3 のAdobe Commerce
* Adobe Commerce オンプレミス 2.0.X、2.1.X、2.2.X、および 2.3.0 ～ 2.3.3

## パッチの適用方法

手順については、を参照してください [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) サポートナレッジベースで。

## 役に立つリンク

* [クラウドインフラストラクチャー上のAdobe Commerceのログファイルの場所スタータープランアーキテクチャ](/help/how-to/general/log-locations-directories-for-starter-plan.md) サポートナレッジベースで。
* [Cloud Infrastructure Pro プランアーキテクチャ上のAdobe Commerceのログファイルの場所](/help/how-to/general/log-locations-directories-for-pro-plan-integration-staging-production.md) サポートナレッジベースで。
* [Adobe Commerceのログファイルの場所](https://devdocs.magento.com/guides/v2.3/cloud/trouble/environments-logs.html) 開発者向けドキュメントを参照してください。

## 添付ファイル
