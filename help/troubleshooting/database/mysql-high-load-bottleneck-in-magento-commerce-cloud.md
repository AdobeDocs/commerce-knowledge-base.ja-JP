---
title: クラウドインフラストラクチャー上のAdobe Commerceにおける MySQL の高負荷ボトルネック
description: ここでは、MySQL からの高負荷が原因で、クラウドインフラストラクチャー上のAdobe Commerceでパフォーマンスがボトルネックになる場合の解決策について説明します。
exl-id: c1f9d282-41d8-4850-8a24-336d55aa3140
feature: Cloud, Observability, Paas, Services
role: Developer
source-git-commit: 075f55b94202f75839abd25bd47824eeb5226485
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# クラウドインフラストラクチャー上のAdobe Commerceにおける MySQL の高負荷ボトルネック

ここでは、MySQL からの高負荷が原因で、クラウドインフラストラクチャー上のAdobe Commerceでパフォーマンスがボトルネックになる場合の解決策について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.x.x 上のAdobe Commerce、Pro アカウント。

### 前提条件

* ECE ツールバージョン 2002.0.16 以降
* New Relic APM サービス （**クラウドインフラストラクチャアカウント上のAdobe Commerceには、New Relic APM サービス用のソフトウェアが含まれます** （ライセンスキーとともに）

New Relic APM サービスおよびお使いのAdobe Commerce on cloud infrastructure アカウントとの設定について詳しくは、以下を参照してください。 [New Relic サービス](https://devdocs.magento.com/guides/v2.3/cloud/project/new-relic.html) および [New Relic APM の概要](https://docs.newrelic.com/docs/apm/new-relic-apm/getting-started/introduction-apm/).

## 問題

<u>問題がユーザーに影響を与えるかどうかを確認する手順</u>

1. New Relicの APM の概要グラフで、MySQL がボトルネックになっていることが最初に示されているかを確認します。 以下のサンプル図を参照してください。ここでは、MySQL がボトルネックとなり、web トランザクション時間の大部分を占めています。

   ![KB-372_image002.png](assets/KB-372_image002.png)

   画像の赤い破線は、MySQL web トランザクションの時間に目に見える上昇傾向を示し、さらに高いレベルでピークを迎えています。
1. ここから、次に **データベース** 高スループットまたは低速の 2 番目の指標を確認できる画面 `SELECT` mysql のクエリ、および以下のサンプル画像では、で並べ替えるときに確認できます。 **最も時間がかかる**&#x200B;この例では、ストアの処理速度が遅くなっています `SELECT` MySQL クエリ

   ![KB-372_image003_BlurredExtension.png](assets/KB-372_image003_BlurredExtension.png)

New Relic APM で低速のトランザクションを分析します。 MySQL データベースに大量のクエリがある、または負荷が高い場合は、を有効にすることで、負荷を様々なノードに分散させることができます。 `SLAVE` 接続。

## 原因：

クラウドインフラストラクチャストア上のAdobe Commerceのスループットが高いか、低速 `SELECT` MySQL クエリ

## 解決策

>[!WARNING]
>
>拡張アーキテクチャ（分割アーキテクチャ）の場合、Redis スレーブ接続 **してはならない** 有効にする。 スケールされたアーキテクチャに準拠しているかどうかを確認するには、プロジェクト URL （例：）に移動します。 `https://console.adobecommerce.com/<owner-user-name>/<project-ID>/<environment-name>`. クリックする **[!UICONTROL SSH]**. ノードが 3 つ以上ある場合は、スケールされたアーキテクチャ上にあります。 スケーリングされたアーキテクチャで Redis スレーブ読み取りを有効にすると、お客様は Redis 接続が接続できないというエラーを受け取ります。 これは、Redis 接続を処理するためにクラスターがどのように設定されているかに関係しています。 Redis スレーブはアクティブですが、Redis 読み取りには使用されません。 Adobe Commerce 2.3.5 以降を使用し、新しい Redis バックエンド設定を実装し、Redis 用の L2 キャッシングを実装するために、スケールアーキテクチャをお勧めします。

この 2 つの兆候が発生した場合は、 `SLAVE` mysql データベースと Redis の接続は、異なるノードに負荷を分散させるのに役立ちます。

Adobe Commerceは、複数のデータベースまたは Redis を非同期で読み取ることができます。 を更新中 `.magento.env.yaml` をに設定してファイルに書き込む `true` 値 `MYSQL_USE_SLAVE_CONNECTION` および `REDIS_USE_SLAVE_CONNECTION` を使用するには **読み取り専用** 非マスターノードで読み取り専用トラフィックを受信するデータベースへの接続。 読み取り/書き込みトラフィックを処理する必要があるのは 1 つのノードのみであるため、ロード・バランシングによってパフォーマンスが向上します。 をに設定 `false` 既存の読み取り専用接続配列を `env.php` ファイル。

### 手順

1. を編集 `.magento.env.yaml` をファイルに保存し、次のコンテンツを追加します。

   ![KB-372_image004.png](assets/KB-372_image004.png)

   詳しくは、こちらを参照してください。 [DevDocs での変数のデプロイ](https://devdocs.magento.com/cloud/env/variables-deploy.html#mysql_use_slave_connection).

1. 変更をコミットし、変更をプッシュします。
1. 変更をプッシュすると、新しいデプロイメントプロセスが開始されます。 デプロイメントが正常に完了したら、Adobe Commerce on cloud infrastructure インスタンスがスレーブ接続を使用するように設定されています。

## よくある質問

クラウドインフラストラクチャストア上のAdobe Commerceにスレーブ接続機能を使用する場合に尋ねられうる一般的な質問を以下に示します。

* スレーブ接続を使用する際の既知の問題や制限はありますか？ **スレーブ接続を使用する際に発生する既知の問題はありません。 最新の ece-tools パッケージを使用していることを確認してください。 説明はにあります [ece-tools パッケージの更新方法](https://devdocs.magento.com/cloud/project/ece-tools-update.html).**
* スレーブ接続を使用して追加のレイテンシーはありますか？ *はい、クロス AZ （クロス可用性ゾーン）の待ち時間は、インスタンスが過負荷でなく、負荷全体を処理できる場合に、クラウドインフラストラクチャインスタンス上のAdobe Commerceのパフォーマンスを低下させます。 ただし、インスタンスが過負荷の場合、マスタースレーブは異なるノードに MySQL データベースまたは Redis の負荷を分散させることで、パフォーマンスの向上に役立ちます。*

  **オーバーロードされていないクラスター上** -  **スレーブ接続では、パフォーマンスが 10～15% 低下します**（デフォルトではない理由の 1 つ）。

  *ただし、過負荷のクラスターでは、トラフィックによる負荷を減らすことで、これらの 10～15% が軽減されるので、パフォーマンスが向上します。*
* ストアに対してこれらの設定を有効にする必要がありますか？ *MySQL データベースまたは Redis の負荷が高い、または高いと予想される場合は、必ずスレーブ接続を有効にする必要があります。 平均トラフィックを使用する通常の顧客の場合、これは次のようになります&#x200B;**ではない**有効にする最適な設定。*

## 関連資料

開発者向けドキュメントでは、

* [変数のデプロイ](https://devdocs.magento.com/cloud/env/variables-deploy.html).
* [オプションのデータベースレプリケーションの設定](https://devdocs.magento.com/guides/v2.3/config-guide/multi-master/multi-master_slavedb.html).
* [ece-tools パッケージ](https://devdocs.magento.com/cloud/reference/ece-tools-reference.html).

>[!NOTE]
>
>この記事には、一部のユーザーが人種差別的、性差別的、または抑圧的と見なす業界標準のソフトウェア用語が依然として含まれており、読者が苦痛を感じたり、トラウマを抱いたり、歓迎されないと感じたりする可能性があることを認識しています。 Adobeでは、これらの用語をアドビのコード、ドキュメントおよびユーザーエクスペリエンスから削除するよう取り組んでいます。
