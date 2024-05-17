---
title: Adobe Commerceに関する Redis のトラブルシューティング
description: この記事は、Redis に関する問題があるAdobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure マーチャント向けのトラブルシューティングツールです。 各質問をクリックすると、トラブルシューティングの各ステップの回答が表示されます。 症状と設定に応じて、バージョンとメモリの問題をトラブルシューティングしてパフォーマンスを最適化する方法を示します。
exl-id: 241abcfd-33b8-449b-b385-32950bd26320
feature: Services, Support
role: Developer
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---

# Adobe Commerceに関する Redis のトラブルシューティング

この記事は、Redis に関する問題があるAdobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure マーチャント向けのトラブルシューティングツールです。 各質問をクリックすると、トラブルシューティングの各ステップの回答が表示されます。 症状に応じて、バージョンとメモリの問題をトラブルシューティングし、パフォーマンスを最適化する方法を示します。

## 手順 1 - Redis の問題 {#step-1}

+++Redis の問題？

a.はい – に進みます。 [手順 2](#step2)</a>.

b.いいえ – に戻る [support.magento.com](https://support.magento.com/hc/en-us) 関連するトラブルシューティング記事を検索します。

+++

## 手順 2 - インストールされている Redis パッチを確認する {#step-2}

+++現在インストールされている Redis パッチ

a.はい – に進みます。 [手順 3](#step3)</a>.

b.いいえ – パッケージの最新バージョンがあることを確認してください `magento-cloud-patches` インストールされています。 このパッケージには、Redis に必要なパッチが含まれています。 アクセスするには、に移動します [GitHub マグネトクラウドパッチ](https://github.com/magento/magento-cloud-patches/).

+++

## 手順 3 - Redis のバージョンがサポートされていることを確認 {#step-3}

+++Redis バージョン 3.2 または 5.0 では？

CLI で次のコマンドを実行して確認します。 プロまたはステージング： `$ redis-cli -p %port-number% info | grep redis_version`、ここで `%port-number%` はポートの番号で、 `app/etc/env.php` ファイルを開くか、次のいずれかのコマンドを実行します。 `$ vendor/bin/ece-tools env:config:show | grep -i redis -A 3` または `$ cat app/etc/env.php | grep redis -A 3` スターターまたは統合： `$ redis-cli -h 'redis.internal' info | grep redis_version`

a.はい – に進みます。 [手順 4](#step4).

b.いいえ。Adobe Commerceは Redis バージョン 3.2 と 5.0 をサポートしています。Adobe Commerceを Cloud Infrastructure 2.3.3 以降で実行している場合は、Redis 5 にアップグレードすることをお勧めします。 マスターブランチを含む Cloud Infrastructure Pro プランアーキテクチャ、Integration、Starter 環境のAdobe Commerceの設定手順については、以下を参照してください。 [クラウドインフラストラクチャー上のAdobe Commerce/Redis サービスの設定](https://devdocs.magento.com/cloud/project/services-redis.html)</a> 開発者向けドキュメントを参照してください。 **必須 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) pro アーキテクチャの実稼動環境およびステージング環境でサービス設定を変更する場合。 また、クラウドインフラストラクチャー上のAdobe CommerceおよびオンプレミスのAdobe Commerce 2.3.5 以降では、拡張 Redis キャッシュの実装をお勧めします。 このタイプの Redis キャッシュ実装は、各Adobe Commerce リクエストで実行される Redis へのクエリの数を最小限に抑える機能強化を提供します。 手順については、次を参照してください [Adobe Commerce 2.3.5 以降の拡張 Redis キャッシュ実装](https://support.magento.com/hc/en-us/articles/360049292532) サポートナレッジベースで。 その他すべてのAdobe Commerce ユーザーについては、を参照してください。 [Adobe Commerce設定ガイド/Redis を設定する](https://devdocs.magento.com/guides/v2.4/config-guide/redis/config-redis.html) 手順については、開発者向けドキュメントを参照してください。

+++

## 手順 4 – 最新バージョンの ECE-Tools を確認する {#step-4}

+++最新バージョンの [ECE ツール > v2002.1.1](https://github.com/magento/ece-tools/releases)?

CLI/ターミナルでコマンドを実行して、使用しているバージョンを確認します。 `$php vendor/bin/composer info magento/ece-tools`.

a.はい – に進みます。 [手順 5](#step5).

b.いいえ –  [ECE ツールのアップグレード](https://devdocs.magento.com/cloud/project/ece-tools-update.html) を最新リリースに更新しました。

+++

## 手順 5 - ネットワークトラフィックの評価 {#step-5}

+++アプリと Redis の間には大量のネットワークトラフィックがありますか？

a.はい – 次を試してください。分割されていないアーキテクチャの場合は、 [セカンダリ接続](/help/troubleshooting/database/mysql-high-load-bottleneck-in-magento-commerce-cloud.md) が使用されます。 分割アーキテクチャの場合、 [L2 キャッシュを有効にする必要があります](https://devdocs.magento.com/guides/v2.4/config-guide/cache/two-level-cache.html).

b.いいえ：次の方法で L2 キャッシュを構成します。 [Redis バックエンドの更新](https://devdocs.magento.com/cloud/env/variables-deploy.html#redis_backend). 次の手順に進みます。 [手順 6](#step6).

+++

## 手順 6 - サイト速度の確認 {#step-6}

+++L2 キャッシュを有効にした後も、サイトの動作が遅いですか？

a.はい – 一時ディレクトリを確認します `/dev/shm` を使用して、スペースを増やす必要があるかどうかを確認します。 さらにスペースが必要な場合は、 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).
b. NO - L2 キャッシュを有効にすると、Redis の問題が解決したようです。

+++

[手順 1 に戻る](#step-1)
