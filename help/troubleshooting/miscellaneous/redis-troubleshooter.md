---
title: Adobe Commerceに関する Redis のトラブルシューティング
description: この記事は、Redis に関する問題があるAdobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure マーチャント向けのトラブルシューティングツールです。 各質問をクリックすると、トラブルシューティングの各ステップの回答が表示されます。 症状と設定に応じて、バージョンとメモリの問題をトラブルシューティングしてパフォーマンスを最適化する方法を示します。
exl-id: 241abcfd-33b8-449b-b385-32950bd26320
feature: Services, Support
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---

# Adobe Commerceに関する Redis のトラブルシューティング

この記事は、Redis に関する問題があるAdobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure マーチャント向けのトラブルシューティングツールです。 各質問をクリックすると、トラブルシューティングの各ステップの回答が表示されます。 症状に応じて、バージョンとメモリの問題をトラブルシューティングし、パフォーマンスを最適化する方法を示します。

## 手順 1 - Redis の問題 {#step-1}

+++Redis の問題？

a.はい – [ 手順 2](#step2)</a> に進みます。

b.いいえ – [support.magento.com](https://support.magento.com/hc/en-us) に戻り、関連するトラブルシューティング記事を検索します。

+++

## 手順 2 - インストールされている Redis パッチを確認する {#step-2}

+++現在インストールされている Redis パッチ

a.はい – [ 手順 3](#step3)</a> に進みます。

b.いいえ – 最新バージョンのパッケージがインストールされていることを確認 `magento-cloud-patches` ます。 このパッケージには、Redis に必要なパッチが含まれています。 アクセスするには、[GitHub magneto-cloud-patches](https://github.com/magento/magento-cloud-patches/) に移動します。

+++

## 手順 3 - Redis のバージョンがサポートされていることを確認 {#step-3}

+++Redis バージョン 3.2 または 5.0 では？

CLI で次のコマンドを実行して確認します。 Pro または Staging: `$ redis-cli -p %port-number% info | grep redis_version`。ここで `%port-number%` はポートの番号です。これは `app/etc/env.php` ファイルに含まれているか、次のコマンドのいずれかを実行して確認できます。`$ vendor/bin/ece-tools env:config:show | grep -i redis -A 3` または `$ cat app/etc/env.php | grep redis -A 3` Starter または Integration: `$ redis-cli -h 'redis.internal' info | grep redis_version`

a.はい – [ 手順 4](#step4) に進みます。

b.いいえ。Adobe Commerceは Redis バージョン 3.2 と 5.0 をサポートしています。Adobe Commerceを Cloud Infrastructure 2.3.3 以降で実行している場合は、Redis 5 にアップグレードすることをお勧めします。 マスターブランチを含む Cloud Infrastructure Pro プランアーキテクチャ、Integration、Starter 環境のAdobe Commerceの設定手順については、開発者向けドキュメントの [Cloud Infrastructure のAdobe Commerce/Redis サービスの設定 ](https://devdocs.magento.com/cloud/project/services-redis.html)</a> を参照してください。 ** Pro アーキテクチャの実稼動環境およびステージング環境でサービス設定を変更するには、[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) する必要があります。 また、クラウドインフラストラクチャー上のAdobe CommerceおよびオンプレミスのAdobe Commerce 2.3.5 以降では、拡張 Redis キャッシュの実装をお勧めします。 このタイプの Redis キャッシュ実装は、各Adobe Commerce リクエストで実行される Redis へのクエリの数を最小限に抑える機能強化を提供します。 手順については、サポートナレッジベースの「[ 拡張 Redis キャッシュ実装Adobe Commerce 2.3.5 以降 ](https://support.magento.com/hc/en-us/articles/360049292532)」を参照してください。 その他のAdobe Commerce ユーザーについては、開発者向けドキュメントの [Adobe Commerce設定ガイド > Redis の設定 ](https://devdocs.magento.com/guides/v2.4/config-guide/redis/config-redis.html) の手順を参照してください。

+++

## 手順 4 – 最新バージョンの ECE-Tools を確認する {#step-4}

+++最新バージョンの [ECE ツール > v2002.1.1](https://github.com/magento/ece-tools/releases) をお持ちですか？

CLI/Terminal: `$php vendor/bin/composer info magento/ece-tools` でコマンドを実行して、使用しているバージョンを確認します。

a.はい – [ 手順 5](#step5) に進みます。

b.いいえ – [ECE-Tools を最新リリースにアップグレード ](https://devdocs.magento.com/cloud/project/ece-tools-update.html) します。

+++

## 手順 5 - ネットワークトラフィックの評価 {#step-5}

+++アプリと Redis の間には大量のネットワークトラフィックがありますか？

a.はい – 次の操作を行ってください。非スプリットアーキテクチャの場合は、[ セカンダリ接続 ](/help/troubleshooting/database/mysql-high-load-bottleneck-in-magento-commerce-cloud.md) が使用されていることを確認します。 スプリットアーキテクチャの場合は、[L2 キャッシュを有効にする必要があります ](https://devdocs.magento.com/guides/v2.4/config-guide/cache/two-level-cache.html)。

b.いいえ – [Redis バックエンドの更新 ](https://devdocs.magento.com/cloud/env/variables-deploy.html#redis_backend) を使用して、L2 キャッシュ設定を構成します。 [ 手順 6](#step6) に進みます。

+++

## 手順 6 - サイト速度の確認 {#step-6}

+++L2 キャッシュを有効にした後も、サイトの動作が遅いですか？

a.はい – 一時ディレクトリの `/dev/shm` をチェックして、容量を増やす必要があるかどうかを確認します。 さらにスペースが必要な場合は、[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) してください。
b. NO - L2 キャッシュを有効にすると、Redis の問題が解決したようです。

+++

[手順 1 に戻る](#step-1)
